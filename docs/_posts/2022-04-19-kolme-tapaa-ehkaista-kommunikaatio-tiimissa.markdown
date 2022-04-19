---
layout: post
title:  "Kolme tapaa ehkäistä kommunikointia tiimissä"
date:   2022-04-19 00:00:00 +0300
readtime: "4min"
---
Miltei jokaista ryhmää, jossa on mukana useampi kehittäjä, kutsutaan tiimiksi. Joskus se voi jäädä juuri sellaiseksi, ryhmäksi toisistaan irrallisia kehittäjiä. Nyt seuraa 2+1 (=3) vinkkiä, jolla voit ylläpitää tätä tilaa! Nämä saattavat perustua johonkin, olen varmasti kuullut näistä muualtakin ja aiheesta saattaa olla tutkittua tietoa, mutta tässä mennään nyt pitkälti kokemuspohjalta.

Eli mikä siis nykyisessä tavassa mättää kommunikoinnin kannalta?

## Optimoi yksilön tuottama arvo

Ajatellaan, että mitä useampi näppäimistö tuottaa yhtäaikaisesti koodia, sitä nopeampaa tuotamme arvoa. Tämä siis käytännössä tarkoittaisi sitä, että koodin kirjoittaminen on se mikä on sovelluskehityksessä hidasta. Ei ole. Ajattelu on sekä hidasta että älyttömän työlästä. Jos kaksinkertaistaisin ajattelutehokkuuteni ja puolittaisin kirjoitusnopeuteni, niin olisin noin tuplasti tehokkaampi koodari.

Toisaalta vaikka minulla olisikin hyvä flow päällä, niin joku toinen tiimissäni saattaa olla samaan aikaan täysin jumissa. Jos muu tiimi on niin kiinni omassa tekemisessään ettei ehdi auttamaan, niin osa tiimiä on täysin tyhjäkäynnillä. Tiesitkö muuten, että jumissa oleminen on todella turhauttavaa. Jos sinulla ei ole ohjelmointikokemusta, niin varmasti olet joskus saanut eteesi matemaattisen tehtävän, josta et tajua yhtään mitään. Vaikka kuinka sitä tavaisit itsellesi, et tule olemaan yhtään sen lähempänä ratkaisua riippumatta kuinka monta tuntia siihen käyttäisit. Sellaista on olla jumissa myös koodatessa, se on se tunne kun et vain osaa.

Toinen mikä on hidasta koodaamisessa on selvittely. Kun ei tiedä miten jokin asia toimii, niin siihen on vaikea tehdä muutoksia. Näppärät testit ja pieni ripaus dokumentoitia voi auttaa tähän ongelmaan, mutta silti selvittelyyn kuluu aikaa. Mutta entä jos olisit itse ollut paikalla, kun ominaisuutta toteutettiin? Väitän, että selvittelyyn käytetty aika vähenisi huomattavasti.


## Tikettien omistaja

Tiketti kuuluu usein vain ja ainoastaan yhdelle tekijälle. Jirassa tms. projektinhallintatyökalussa on naamakuva tiketissä, jonka työstössä jokin asia on. Se on sitten hänen. Siihen älkööt muut koskeko. Ja kun muilla tiimin jäsenillä on jo oma tiketti, niin onko OK olla itse ilman?

Ajatuksena koko touhussa lienee se, että jos tiketillä ei ole omistajaa eikä se ole kenenkään vastuulla, ei sitä kukaan myöskään tee. Tämä varmasti pätee hyvin paikoissa, jossa vallitsee epäluottamuksen ilmapiiri tai tiimi koostu MVP (minimum viable programmer) tekijöistä, jotka tekevät juuri ja juuri sen mitä pyydetään.

Ongelma tässä on mielestäni se, että tapa on omiaan estämään yhteistyön. Jälleen menetetään paikka tiimityölle ja keskustelulle. Mitä jos jokin taski olisikin kahden tai useamman tekijän vastuulla? Molempien pitäisi silloin tietää ominaisuudesta ja toteuttaa sitä aktiivisesti yhdessä. Samaan aikaan aiheesta syntyisi keskustelua ja tekijät voisivat oppia toinen toisiltaan.

Tiketin omistajuus johtaa helposti siihen, että sovellusta tehdään kokoajan eteenpäin usealla rintamalla. Keskeneräistä työtä on kokoajan jollakin kehittäjällä meneillään. Tämä voi johtaa siihen, että julkaisua tulee kiusaus viivästyttää ja lisätä siihen aina yksi *ihan just valmis* ominaisuus. Lopuksi toivotaan, että palaset loksahtavat paikalleen. Onkohan muuten kenelläkään muulla tästä kokemusta?


## Merge request

Merge request käytäntö on muodostunut versiohallinnan käytön menetelmäksi, jossa toinen (riippumaton) tekijä katselmoi toisen tekijän koodin. Käytäntö lienee tullut open source maailmasta, jossa tekijöitä saattaa olla esimerkiksi eri aikavyöhykkeeltä.

Ajatuksena tässä on saada versiohallinnan päähaaraan ainoastaan laadukasta tavaraa ja siihen on tarjottu lääkkeenä koodikatselmointia päähaaraan liittämisen yhteydessä. Ominaisuutta toteutettaessa on usein sokea omille virheilleen, joten toisen silmäparin on tarkoitus huomata ne tekemäsi virheet. Tapana tämä on kommunikaation kannalta aavistuksen parempi kuin se perinteinen koodikatselmointi, jossa sovellusta on tahkottu vaikkapa puoli vuotta, jonka jälkeen kutsutaan ekspertti paikalle. Sitten expertti kertoo, mitkä kaikki asiat koodissa on pielessä. Kiitos avusta.

Merge request käytännössä yhtenä ongelmana voi olla se, ettei kukaan kerro, mikä on pielessä. Eikä katselmoijalla välttämättä ole edes tarpeeksi tietoa siitä, mitä ominaisuudella halutaan. Miten arvioida sellaista, josta ei tiedä miten sen tulisi toimia? Parhaimmillaankin tällä käytännöllä saadaan kiinni pieniä lapsuksia, harvemmin mitään merkittävää.

Ehkä kuitenkin suurin ongelma on se, että kommunikoinnin tapa on tässä kommentoivaa eikä keskustelevaa. Jos kommunikointi työstä on vain tätä, se on herkästi "nillittämistä". Katselmointi siis tehdään aina vasta siinä vaiheessa kun työ on jo valmis. Eli vaihtoehdot kärjistetysti ovat joko nillittää pikku jutuista tai antaa kaiken mennä. Kumpikaan vaihtoehto ei ole kommunikaation kannalta kovin hedelmällinen.

## Mitä sitten? Näinhän meillä on aina tehty

Nämä kaikki kohdat tähtäävät siihen, että sovellusta voitaisiin tehdä mahdollisimman vähäisellä määrällä keskustelua. Vaikkakin tarkoitusperät ovat ehkä hyvät, niin ne eivät palvele millään tavalla aitoa yhdessä tekemistä. Jos kommunikointi työstä tapahtuu aina vasta työn valmistuttua, niin mitä todennäköisimmin tiimisi kommunikointitilanteet ovat kaikki arvostelutilanteita. Aivan varmasti se harmittaa taitelijaa saada kritiikkiä työstä, johon hän on käyttänyt niin paljon aikaa ja vaivaa.

Suunnittelin alunperin, että olisin tähän kertonut, mitä voisi tehdä toisin. Jätän nyt kuitenkin tämän tällaiseen negatiiviseen tilaan, pahoittelut siitä. Mutta onpahan sitten seuraavallekin tekstille jo valmis aihe!

Jos et aio sitä lukea niin sen viesti on, että kannattaa työskennellä enemmän tiimin kanssa yhdessä.