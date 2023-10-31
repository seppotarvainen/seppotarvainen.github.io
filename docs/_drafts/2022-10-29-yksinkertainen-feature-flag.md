---
layout: post
title:  "Feature flag Angular sovellukseen"
date:   2023-10-29 12:30:00 +0300
readtime: "4min"
---

<!-- excerpt-end -->

Omassa tiimissämme toistaiseksi riittää kun voimme erottaa ominaisuudet jotka:
- ovat kesken, mutta julkaistaan tulevaisuudessa
- helpottavat kehitystyötä, mutta ei koskaan julkaista
- helpottavat e2e testausta, mutta ei koskaan julkaista

Tätä varten voidaan kirjoittaa esimerkiksi oma enum:

```ts
/**
 * WipFeature  = Work in progress, released in the future
 * DevFeature  = Improves developer experience, will never be released
 * TestFeature = Improves e2e testing, will never be released
 */
export enum Feature {
  DEV_FEATURE = "devFeature",
  TEST_FEATURE = "testFeature",
  WIP_FEATURE = "wipFeature",
}
```

Tiedot tulee hakea palvelimelta, eli siellä tulee olla endpoint, joka vastaa kirjautumattomalle käyttäjälle tiedot käytössä olevista ominaisuuksista.

```ts

export const ENV_SESSION_STORAGE_KEY = "ymparistoAsetukset";

@Injectable()
export class EnvironmentService {

  private envSettings: EnvironmentSettings;

  constructor(localStorage: LocalStoragePort) {
    const settings = localStorage.getItem(ENV_SESSION_STORAGE_KEY);
    this.envSettings = new EnvironmentSettings(JSON.parse(settings));
  }

  get environment(): string {
    return this.envSettings.env;
  }

  public isFeatureEnabled(feature: Feature): boolean {
    return this.envSettings.features.has(feature);
  }
}
```

Angularin käynnistyessä tulee `main.ts`-tiedostossa hakea flagit palvelimelta:

```ts
import {enableProdMode} from '@angular/core';
import {platformBrowserDynamic} from '@angular/platform-browser-dynamic';
import {AppModule} from './app/app.module';
import {ENV_SESSION_STORAGE_KEY} from "./env/environment.service";


fetch("/api/url/to/your/feature/flags")
  .then(response => response.text())
  .then((response: string) => {
  	const featureInfo = JSON.parse(response); 
  	// implement your logic
  });
 ```

