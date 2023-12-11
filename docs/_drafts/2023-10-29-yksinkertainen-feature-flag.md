---
layout: post
title:  "Feature flagit Angular-sovelluksessa"
date:   2023-11-29 12:30:00 +0300
readtime: "4min"
---

Päähaarassa kehittäminen (Trunk based development) vaatii aina jonkinlaisen tavan erottaa keskeneräinen ja julkaistava työ toisistaan. Siihen löytynee monia keinoja, mutta yksi helpoimmista lienee feature flagien käyttö. Niidenkin käytössä on kuitenkin nyansseja. Ne voivat olla  käännöksen aikana luotuja tai niitä voidaan muokata ajon aikana. Se, kuinka dynaamisia niistä tarvitset, riippuu sovelluksestasi. Meidän tiimissä ainakin toistaiseksi pärjätään käännöksen aikaisilla flageilla. 

<!-- excerpt-end -->

Ennen kuin ryhdyt tekemään omia räätälöityjä ratkaisua, tarkista olemassa olevat tuotteet. Esim. GitLab-CI:ltä löytyy feature flagit ja on niiden hallintaan tehty ihan omia sovelluksiakin[^1]. Me päädyimme tekemään oman ratkaisun ja halusimme erottaa toisistaan ominaisuudet jotka:

- Ovat kesken, mutta julkaistaan tulevaisuudessa.
- Helpottavat kehitystyötä, mutta joita ei koskaan julkaista.
- Helpottavat e2e testausta, mutta joita ei koskaan julkaista.

Ensin määritellään ominaisuuden toiminnallisuus kirjoittamalla testi. Tiesimme, että tulemme käyttämään `localStoragea`, jonka vuoksi `storage`-muuttuja matkii sen toiminnallisuutta.

```ts
describe('EnvironmentService', () => {

  it('should have wipFeature', () => {
    const storage = {getItem: () => "{features: ['wipFeature']}"}

    const env = new EnvironmentService(storage);

    expect(env.isFeatureEnabled(Feature.WIP_FEATURE)).toBeTruthy();
    expect(env.isFeatureEnabled(Feature.DEV_FEATURE)).toBeFalsy();
    expect(env.isFeatureEnabled(Feature.TEST_FEATURE)).toBeFalsy();
  });

});
```

Toteutus on tämän jälkeen aika yksinkertainen. Enum selkeyttää ratkaisua ja koodista löydetään helpommin flagien käyttö:

```ts
/**
 * WipFeature  = Work in progress, released in the future
 * DevFeature  = Improves developer experience, will never be released
 * TestFeature = Improves e2e testing, will never be released
 */
export enum Feature {
  WIP_FEATURE = "wipFeature",
  DEV_FEATURE = "devFeature",
  TEST_FEATURE = "testFeature"
}
```

`EnvironmentSettings` -luokka hoitaa sisäisesti JSON-muotoisen datan käsittelyn ja `EnvironmentService`-objektia käytetään apuna tarkistamaan flagien käyttö.

```ts
export const ENV_SESSION_STORAGE_KEY = "envSettings";

@Injectable()
export class EnvironmentService {

  private envSettings: EnvironmentSettings;

  constructor() {
    const settings = localStorage.getItem(ENV_SESSION_STORAGE_KEY);
    this.envSettings = new EnvironmentSettings(JSON.parse(settings));
  }

  public isFeatureEnabled(feature: Feature): boolean {
    return this.envSettings.features.has(feature); // 'this.envSettings.features' on tässä ihan tavallinen Set<string>
  }
}
```

1. `ENV_SESSION_STORAGE_KEY` on julistettu ulospäin, jotta varmasti samaa avainta voitaisiin käyttää sovelluksen käynnistyessä.
2. `@Injectable` määritys lisätty, jotta ratkaisua voidaan käyttää Angularin *dependency injection* -toteutuksen kanssa.

Ylläolevassa koodissa ongelmana on sen riippuvuus globaalista `localStorage`-muuttujasta. `localStorage` on *ulkoinen palvelu*, eikä se kuulu meidän domainiin, joten sitä ei tulisi kirjoittaa suoraan domain-luokan sisään. Angularin DI toteutus ei kuitenkaan hyväksy oletusparametreja ja toisaalta helppokäyttöisyyden vuoksi haluan mieluummin kirjoittaa `new EnvironmentService()` sen sijaan, että se aina annettaisiin erikseen parametrina: `new EnvironmentService(localStorage)`

Angularin käynnistyessä haetaan `main.ts`-tiedostossa flagit palvelimelta:

```ts
import {enableProdMode} from '@angular/core';
import {platformBrowserDynamic} from '@angular/platform-browser-dynamic';
import {AppModule} from './app/app.module';
import {ENV_SESSION_STORAGE_KEY} from "./env/environment.service";


fetch("/api/url/to/your/feature/flags")
  .then(response => response.text())
  .then((response: string) => {
    localStorage.setItem(ENV_SESSION_STORAGE_KEY, response);
    // rest of the logic
  });
```

Kun flagit on haettu palvelimelta ne voidaan ottaa käyttöön parhaaksi katsomalla tavalla. Me lisäsimme direktiivit, joita voidaan käyttää template-tiedostoissa. Mikäli feature flagien käyttö jossain vaiheessa tulee hienojakoisemmaksi, voidaan kirjoittaa yksi direktiivi, jolle annetaan parametrina `Feature`.

```ts
@Directive({
  selector: '[wipFeature]'
})
export class WipFeatureDirective implements OnInit {

  constructor(private elementRef: ElementRef,
              private environmentService: EnvironmentService) {
  }

  ngOnInit(): void {
    if (!this.environmentService.isFeatureEnabled(Feature.WIP_FEATURE)) {
      this.elementRef.nativeElement.remove();
    }
  }

}
```

Käyttö templatessa:

```html
<div wipFeature>
  <p>This is hidden from production</p>
</div>
```

Käyttö muualla koodissa suoraan `EnvironmentService`-objektin kautta:

```ts
export class MyComponent {

  const env = new EnvironmentService();

  someKindOfFunctionality() {
    if (env.isFeatureEnabled(Feature.WIP_FEATURE)) {
      return 'This is a work in progress'
    }
    return 'This work is published';
  }

}
```

Kun ominaisuus halutaan julkaista, poistetaan flagin käyttö ko. ominaisuudelta.

En ole edelleenkään ihan varma olisko `isFeatureDisabled` sittenkin parempi nimi funktiolle kuin `isFeatureEnabled`? Vai pitäisikö olla molemmat?

___

[^1]: [https://www.g2.com/categories/feature-management](https://www.g2.com/categories/feature-management)
