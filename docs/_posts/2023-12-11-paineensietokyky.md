---
layout: post
title:  "Koodisankarit"
date:   2023-12-11 00:00:00 +0300
readtime: "4min"
---

Olen ennen ollut ylpeä siitä, kuinka hyvin olen sietänyt painetta. Voin tiukassakin tilanteessa toimia ja *vaikuttaa* rauhalliselta, vaikka kuinka sisälläni kuohuisi. Tästä taidosta on kuitenkin turvallisessa ja hyvin toimivassa tiimissä myös haittaa. Pääsääntöisesti painetta nimittäin ei tulisi sietää, vaan se tulisi poistaa.

<!-- excerpt-end -->

## Sankarikoodareiden perisynti

Meillä ei tulisi olla tarvetta harjoittaa itsellemme korkeaa paineensietokykyä. Hyvällä sietokyvyllä varustetut tekijät kestävät kaaosta, huonolaautista koodia, olematonta arkkitehtuuria, kiirettä ja kaikkea sitä, mikä tekee sovelluskehittäjän työstä stressaavan. Edellä mainittuja asioita ei tule kestää, sillä niin kauan kuin siedän jotain, en tee mitään ongelman juurisyyn korjaamisen eteen. On täytynyt ihan harjoitella sitä, että kun huomaan jonkin asian olevan pielessä, korjaan sen nyt. En siis vasta silloin, kun se jo aiheuttaa ongelmia.

Ehkä pahinta on se, että tällaisia henkilöitä katsotaan työelämässä ylöspäin. He saavat aikaan näkyvää muutosta nopeasti, puhuvat kieltä jota juuri kukaan muu ei ymmärrä ja sammuttavat tulipalot tuotannossa salamannopeasti. Yksi syy tähän salamannopeuteen voi olla se, että tämä sankari on alunperin aikaansaanut ko. virhetilanteen koodiin. Sankari ei kuitenkaan kerro sitä muille. Se himmentäisi sädekehää.

Pahempaa kuin tehdä tietämättömyyttään huonoja tai "väliaikaisia" ratkaisuja on tehdä niitä täysin tietoisesti. Kovassa liemessä keitetyt, maailmaa nähneet, painekattilassa karaistut sankarikehittäjät eivät ole niitä tekijöitä, jotka saavat suunnan kääntymään paremmaksi. Toisinaan pitkään alalla olleet ovat valitettavasti ehtineet jo tottua heikkolaatuiseen koodiin, jonka parissa he pystyvät uimaan sujuvasti. He saattavat nousta sankariasemaan, eli henkilöiksi, jotka tiukan paikan tullen saavat aina viritettyä jonkinlaisen toimivalta vaikuttavan ratkaisun. Sankarina oleminen on kuitenkin enemmän luonteenpiirre kuin jokin kokemusvuosien perusteella pääteltävä  ominaisuus.

## Seniori vs. Sankari

Se, että henkilö on ollut alalla pitkään, ei tee hänestä automaattisesti välinpitämätöntä sankarikehittäjää. Todellinen osaaja, eli ihan aito *Senior Software Engineer* edesauttaa tuotteen kehitystä laadultaan paremmaksi joka ikinen (työ)päivä. Ainoa paine, jota on hyödyllistä sietää, on kehitystiimin ulkopuolelta tuleva aikataulupaine. Tällaisen paineen edessä tulee kertoa rehellisesti oma arvio siitä, kuinka kauan haluttu ominaisuus vie aikaa. Kun sen jälkeen kysytään, "voiko sen tehdä nopeammin, jos tällä kertaa jätetään testausta vähemmälle", niin vastauksen tulisi olla "parempi on jättää ominaisuus tekemättä, jos sitä ei edes vaivauduta testaamaan." . 

Seniori pyrkii tekniseen erinomaisuuteen. Hän aktiivisesti harjoittaa testivetoista kehittämistä, edesauttaa jatkuvaa integraatiota ja jatkuvaa toimittamista. Kun näiden minimivaatimukset tiimissä on saavutettu, seniorikehittäjä tutkii keinoja yhdessä tiimin kanssa miten niitä voidaan toteuttaa entistäkin paremmin. Seniori kokeilee, oppii kokeiluistaan, jakaa oppimaansa muille ja oppii muiden kanssa.

Seniori keskustelee eri asiantuntijoiden ja liiketoiminnan kanssa. Hän pyrkii ymmärtämään todellista tarvetta, eikä vain tee sitä mitä käsketään. Seniori optimoi tekemättömän työn määrää. Eli vähemmän radikaalisti imaistuna: "Seniori ei tee turhaa työtä". 

Mikäli eri sidosryhmien välillä on kommunikaatiossa ongelmia, seniori yrittää etsiä niihin ratkaisua. Tämä silloinkin, kun syy ei ole hänessä itsessään tai tiimissä. Kaikki mikä hidastaa tai hankaloittaa tiimin työskentelyä, on seniorille haaste joka tulee ratkaista. Seniori ei sysää vastuuta tekemisistään mihinkään ulkopuolelle, vaan kantaa päätöksistään vastuun. On hän sitten konsultti tai yrityksen omaa väkeä.

Se mikä voi näyttää ulospäin tuottavalta, voi todellisuudessa olla vain hetkellinen laastari ongelmaan. Kun virheitä jossain kohtaa ilmenee, sankarikoodari saa ratkaisun tehtyä nopeasti. Seniorikoodari löytää ongelman samassa ajassa, mutta hän käyttää aikaa myös siihen, ettei virhe toistu enää koskaan. Kun virhe on löydetty, seniorikoodari kirjoittaa testin sovelluksen toivottua tilaa vasten. Vasta tämän jälkeen hän tekee korjauksen.

Jos sankarikulttuuria pidetään yllä, tulipaloihin ajan saatossa totutaan. Ajatellaan, että on ihan luonnollista kun kokoajan vähän palaa metsää. Palon yltyessä painetaan paniikkinappulaa ja rukoillaan sankarin saapuvan paikalle. Palo tulee sammutetuksi ja seuraavalla kerralla siviilit jälleen luottavat siihen, että sankari ennättää paikalle, kun tarvetta on. He eivät edelleenkään osaa toimia metsäpalon sattuessa. Eivätkä he todellakaan etsi syitä siihen, miksi metsäpalot yleistyvät.

Seniori ei harmittele, jos hänen kallisarvoista aikaa kuluu myös tuoreempien kehittäjien mentorointiin. Kehitystiimissä seniorilla ei ole "omia" tehtäviä, vaan tehtävät ovat tiimin yhteisiä. Seniori opettaa muita tiimin jäseniä paremmiksi kehittäjiksi ja koodaa vähemmän itse. Jos seniori jossain kohti jatkaa muihin haasteisiin, hänen ei tarvitse pitää tiimille lähtiessään luentoa siitä, miten tuotteen eri komponentit toimivat. Kun sankari lähtee muihin haasteisiin, ei siviiliuhreilta voida välttyä.

## Saako siis sankari enemmän aikaan?

Saa, tuhoa nimittäin. Jos tittelisi osana on "Senior" ja jotain, ole hyvä ja tee työsi sen mukaisesti. Jos haluat sankarin viitan, pyydä tittelisi muutoksta sankarikoodariksi. Silloin kaikki voivat kutsua sinua yhdenlaiseksi "sankariksi".