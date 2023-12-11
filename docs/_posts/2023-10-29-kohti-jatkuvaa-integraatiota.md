---
layout: post
title:  "Kohti jatkuvaa integraatiota"
date:   2023-10-29 12:30:00 +0300
readtime: "4min"
---

Yksi merkittävimpiä valaistumisen kokemuksia ohjelmistokehityksessä oli ymmärtää, ettei CI ole mikään *putki*. Jatkuva integraatio ei ole tekninen ongelma eikä sitä voi yksinään millään teknisellä vippaskonstilla ratkaista. Jatkuva integraatio on toimintatapa. Sen keskiössä on hyvin toimiva tiimi, jota avustaa automaatio. Ja ennen kaikkea, tämä hyvin toimiva tiimi tuottaa laadukasta softaa yhdessä.

<!-- excerpt-end -->

Jos olet aikeissa toteuttaa jatkuvaa integraatiota, niin muutoksessa on syytä lähteä [minimistä](https://minimumcd.org/minimumcd/). Minimivaatimukset jatkuvalle integraatiolle ovat[^1]:

- Päähaarassa kehittäminen (Trunk-based development)
- Työ integroidaan päähaaraan vähintään päivittäin
- Työ testataan automaattisesti ennen päähaaraan yhdistämistä
- Työ testataan muun työn kanssa automaattisesti haaroja yhdistettäessä
- Kaikki uuskehitys loppuu, kun integroimisputki on punaisella
- Uusi työ ei riko toimitettua työtä

Muutosta on todennäköisesti luvassa, mikäli moiseen ryhtyy. Suosittelen lähtemään sieltä missä tiimillänne on selkeästi parannettavaa ja miettiä, miten muutos voidaan saada aikaiseksi. Meidän osalta merkittävin muutos oli siirtyä featurehaaroista päähaarassa kehittämiseen.

## Hyvästi Git flow

Olen ollut Git flown harjoittaja jo pitkään ja ajattelin, ettei parempaa tapaa voi koskaan tullakaan. Ennen kuin ymmärsin Git flown, sain versionhallinnan tämän tästä solmuun. Onnistuin siinä jopa omissa harrasteprojekteissa. Opittuani sen kaikki oli yhtäkkiä selvää.

Git flow on alalla de facto prosessi, jota noudatetaan laajalti. Sen ideana on mahdollistaa työn eteneminen asynkronisessa ympäristössä, esim. avoimen lähdekoodin projekteissa, joissa tekijät ovat eri aikavyöhykkeiltä ja tekevät sovellusta enemmän tai vähemmän harrastuksena. Siinä on kaksi päähaaraa: *master* ja *develop*. Sen lisäksi löytyvät feature haarat, joissa toiminnallisuuksia tehdään. Kun ominaisuus on valmis, se joko liitetään develop-haaraan tai hylätään. Prosessiin liittyy vielä olennaisena osana release-haarat ja tarvittaessa hotfix-haarat, joita sitten liitetään developiin ja masteriin.

Git flow mahdollistaa sovelluksen yhtäaikaisen kehittämisen siten, ettei tekijöiden tarvitse tietää muiden tiimiläisten tekemisistä juuri mitään. Tämä on Git flown huonoin ominaisuus, kun tehdään ammattimaisesti softaa kehitystiiminä. Aivan kuin sillä olisi mitään merkitystä, kuinka monta näppäimistöä naputtaa koodia yhtäaikaa. Ohjelmistokehityksessä ei ratkaise näppäilynopeus vaan se, kuinka paljon kehittäjät ymmärtävät siitä mitä ovat tekemässä. Tiedonjakaminen lisää tätä ymmärrystä ja sen edistämiseksi pari- ja ryhmäkoodaus soveltuvat mainiosti.

Trunk-based development eli päähaarassa kehittäminen tarkoittaa sitä, että kehitys tapahtuu yhdessä versionhallinnan haarassa. Tämä tapa kannustaa pari- ja ryhmäkoodaamiseen ja käytännössä poistaa merge konfliktit kokonaan. Vaikeinta Trunk-based developmentissa on luopua vanhoista tottumuksista. Aiemmin ominaisuutta saattoi kehittää niin kauan kunnes se olisi valmis, mutta nyt kehitettävä toiminnallisuus majailee aikansa keskeneräisenä versiohallinnan päähaarassa. Tämän vuoksi TBD on muutakin kuin branchaus strategia, sillä se vaatii mahdollisuuden erottaa keskeneräisen työn julkaistavasta työstä.

## Feature flagien toteutus

Ennen kuin voisimme kehittää sovellustamme päähaarassa, tarvitsimme toimivat mekanismit ominaisuuksien piilottamiselle. Git flow’ssa tämä asia hoidettiin pääasiassa release-haarojen avulla, mutta uudessa tavassa release-haaroista oli päästävä eroon. Meidän ratkaisuksi muodostuivat feature-flagit.

Sovelluksestamme löytyi jo entuudestaan tavat piilottaa asioita asiakassovelluksen puolelta, mutta päätimme kuitenkin kirjoittaa sen kokonaan uusiksi. Emme tässä kohtaa halunneet tehdä ominaisuudesta dynaamista, vaan piilottaminen ja julkaisu tapahtuisivat tuotantoonviennin yhteydessä. Kirjoitimme kuitenkin ominaisuuden sellaiseksi, että featureflagit ja niiden käyttö tapahtuu yhdestä paikasta. Myös koodissa featureflageihin viitataan keskitetystä paikasta, jotta niiden käytön seuraaminen on helpompaa.

Aiemmassa tavassamme featureflagit asuivat asiakassovelluksen env-määrityksissä, jotka asetettiin käännösaikana. Tästä syystä client tuli buildata oikeassa ympäristössä, jotta määritykset tulivat voimaan. Nyt sovelluksemme käännetään vain kerran ja kun ympäristömuuttujissa on tiedossa oikea profiili, saadaan oikeat flagit mukaan ympäristökohtaisesti.

## Päivittäiset rutiinit kuntoon

Kun keskeneräisen ominaisuuden voi helposti piilottaa, eikä se luo joka kerta ylimääräistä monimutkaisuutta sovelluskoodiin, päähaarassa kehittäminen on ainakin teoriassa mahdollista. Viimeinen opeteltava asia on muistaa tehdä commit päähaaraan vähintään päivittäin, mutta mieluummin sitäkin useammin.

Mikäli tämä tapa on tiukassa juurtua, voit alkuun kokeilla laittaa itsellesi työpäivän päätteeksi vaikka herätyskellon soimaan mergen merkiksi. Meillä on töissä käytössä Slack, joten ajastin tämän viestin itselleni kaikkiin arkipäiviin klo 15:30.

> Ei tarvi olla valmis, mutta tee se commit!

Nyt sen muistaa jo tehdä ilmankin.

___

[^1]: Suora lainaus täältä: [https://minimumcd.org/minimumcd/](https://minimumcd.org/minimumcd/). Sivustolla määritellään minimiehdot CI/CD:lle ja ohjeistetaan, miten prosessin voi aloittaa.
