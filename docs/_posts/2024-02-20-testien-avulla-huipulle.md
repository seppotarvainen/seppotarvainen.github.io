---
layout: post
title:  "Testien avulla huipulle"
date:   2024-02-20 03:00:00 +0300
readtime: "5min"
---

Useammin kuin kerran tai kaksi, olen kuullut kehotuksia siitä, että testausta olisi syytä jättää vähemmälle nopeamman sovelluskehityksen toivossa. Toisinaan tämä pyyntö on tullut henkilöiltä, joilla ei ole teknistä taustaa. Näissä tilanteissa ymmärrän tämän pyynnön täysin ja minun on ollut vaikea kertoa ymmärrettävästi, mitä hyötyä testien kirjoittamisesta on sovelluskehityksessä. Sorrun helposti selityksissäni koodin ylläpidettävyyteen, refaktoroinnin mahdollistamiseen tai vaikkapa siihen kuinka testit dokumentoivat sovelluskoodin käyttöä. Oikeita asioita sinällään, mutta näistä ajatuksista kiinni saaminen on vaikeaa, mikäli henkilöllä itsellään ei ole kosketusta käytännön sovelluskehitykseen. Onneksi keksin täydellisen vertauskuvan, jonka kautta voin kertoa testauksen hyödyistä... nyt harmittaa mikäli tämä ei olekaan omani.

<!-- excerpt-end -->

## Kalliokiipeilijän testit

Laita silmät kiinni ja kuvittele mielessäsi taitava kiipeilijä korkean kallioseinämän eteen. Oletan, että jossain kohtaa avaat silmäsi. Luonnollisesti kiipeilijällä on tarkoitus kiivetä seinämän huipulle ja ottaa sieltä hienoja kuvia, postata ne johonkin sosiaaliseen mediaan ja saada tutut ja tuntemattomat kateellisiksi hänen hienosta suorituksestaan. Olkoon motiivit mitkä vain, hän on päättänyt kiivetä huipulle.

Luonnollisesti kiipeilijällä on turvanaan köysi ja hänellä on mahdollisuus asettaa seinämään erilaisia kiinnikkeitä. En muuten tiedä kalliokiipeilyn termeistä mitään ja miten se tarkalleen ottaen toimii, mutta oletan että ensimmäisenä kipuavan on jotain kiiloja tms. laitettava kiivettävään kohteeseen. Ajatusleikin vuoksi, kuvitellaan että kiipeilijällä on tarvittavat työvälineet ja osaaminen näiden kiinnitysten tekoon.

Kiipeilijä pääsisi huipulle nopeammin, mikäli hän ei käyttäisi mihinkään ylimääräiseen varmistamiseen aikaa. Onnistuessaan lopputulos on sama ilman varmistusta tai sen kanssa. Virhetilanteessa lopputulos on toisaalta hyvinkin erilainen, riippuen lähinnä siitä millä korkeudella virhe tulee tehtyä. Kiipeilijä tekee varmistuksia putoamisen varalta, sillä hän voi kuvitella tekevänsä kohtalokkaan virheen jollain tulevalla askelmalla. Kiipeilijä ei esimerkiksi asettele kallioon lihan palasia mahdollisia verenhimoisia korppikotkia hämätäkseen. Niitä hän ei osaa kuvitella tulevan vastaan. Sovelluskehityksessäkin testit estävät nimenomaan ne virhetilanteet, jotka ovat kuviteltavissa ennakkoon. 

Testaus ei ole siis sitä varten, että koodista löydettäisiin sitä tehdessä odottamattomia virheitä. Suurin osa testeistä ovat esimerkkipohjaisia, tarkoittaen sitä, että niissä on ennalta määrätty alkuasetelma, suoritus ja tarkistus. Leikitään, että testaan koodin pätkää (=funktiota), joka muuttaa sanan pienet kirjaimet isoiksi. Käytän tätä esimerkkiä myös myöhemmin tässä kirjoituksessa, joten selkeyden vuoksi annan tuolle funktiolle nimeksi `shout`. Kun annan sille syötteeksi `testi` haluan testata, että lopputulema on `TESTI`. Tuolla esimerkillä en saa kaikkia mahdollisia virhetilanteita kiinni, vaan varmistan ainoastaan tuon yhden tapauksen toimivaksi. Voin kuitenkin olettaa, että todennäköisesti kaikki muutkin pienaakkoset toimivat, ehkä skandimerkit voisi testata vielä erikseen. Kuinka kestävän turvaköyden haluan testini muodostavan riippuu kyvystäni kuvitella eri testitapauksia ja siitä, kuinka todennäköisenä jotain virhetilannetta pidän. Voin testeillä tarkistaa reunatapauksia ja todentaa, ettei koodini hätkähdä esimerkiksi numeerisia merkkejä tai välilyöntiä. Haluan ehkä myös luoda testin, joka testaa funktiota täysin tyhjällä merkkijonolla.

## Puoliväliin jätetty varmistus

Kuvitellaan jo aiemmin meille tutuksi tullutta kiipeilijää. Hän aloittaa kiipeilynsä ja varmistaa turvallisuutensa matkalla. Kiipeilijän ollessa puolimatkassa hänelle huudetaan huipulta, että nuotiomakkara odottaa valmiina, eikä se pysy lämpimänä enää pitkään. Kiipeilijälle tulee kiire ja hän säästää aikaa jättämällä loppumatkasta varmistukset tekemättä. Lähellä huippua aiemmilla kiinnikkeillä ei tee enää mitään, sillä otteen livetessä kiipeilijän vyötäisillä oleva köysi yltää jo maahan asti.

Sovellusta kehitettäessä käy samoin, mikäli testaus jätetään huomiotta jossain kohtaa kehitystä. Testit eivät enää testaa sitä sovellusta, millainen se oli niiden kirjoitushetkellä. Jos ne ovat jääneet vähälle huomiolle, on ymmärrettävää, että niiden ylläpidosta koituu ylimääräistä harmia ja kustannuksia. Ne saattavat osoittaa virheitä siellä, missä niitä ei todellisuudessa ole, ne voivat toimia eri tavoin eri suorituskerroilla ja kaikkea mitä vain voit kuvitella. Niimpä niitä ei enää tehdä ollenkaan ja syntyy ajatus, että testaaminen on kallista ja turhaa.

Palataan kiipeilijään. Ajatellaan nyt, että hän olisi jättänyt joka toisen varmistuksistaan tekemättä. Voi olla, että otteen livetessä hän ei menehdy, mutta silti tippuminen saattaa tuottaa tuskaa ja ehkä jopa aiheuttaa loukkaantumisen. Tällaista on heikko tai vaillinainen testaus myös sovelluskehityksessä. Testaus ei enää estäkään edes sellaisia virhetilanteita, joita voitiin kuvitella etukäteen. Kiipeilijäkin taatusti ymmärtää, että ote voi livetä missä kohtaa tahansa. Myös sovelluksessa virhe voi olla kätketty aivan minne tahansa, missä on yhtään minkäänlaista logiikkaa.

## Merkitty reitti

Tiedossa olevien virheiden estämisen lisäksi testit dokumentoivat tapaa, miten sovelluksen koodia käytetään. Aivan kuten kiipeilijän jättämät kiinnikkeet kallioseinämään auttavat tulevia kiipeilijöitä suoriutumaan seinämästä nopeammin. Jos kiinnikkeitä ei ole, jokaisen kiipeilijän tulee itse selvittää, miten seinämä kivutaan ylös. Toki joku saattaa olla antamassa vinkkejä suoritukseen tai miksei siitä voisi kirjoittaa erillisiä ohjeitakin. Näin toimitaan tietysti myös sovelluskehityksessä. Mielelläni silti näkisin ne kiinnikkeet valmiina siellä kalliossa.

## Muutokset reitillä

Vielä viimeisen kerran kuvitellaan tuo kiipeilijä. Hän huomaa kesken matkan, ettei reitti huipulle ole se mitä hän ajatteli. Hän joutuu siirtymään huomattavasti sivummalle, jolloin köyden ja kiinnitysten välille muodostuu ylimääräistä kitkaa eikä liikkuminen oikein tahdo sujua. On selvää, että myös sovelluskehityksessä testien tulee muuttua, mikäli johonkin toiminnallisuuteen halutaan sisällöllistä muutosta. Jos vaikka aiemman `shout`-funktion ei enää pidäkään muuttaa kirjaimia isoksi, vaan lisätä loppuun huutomerkki, niin toki tällöin testikin kaipaa muutosta. Koska nimesin funktioni hienosti, minun ei tarvitse muuttaa testissäni kuin sen tarkistusosuutta. Mikäli nimi olisi aiemmin ollut `toUpperCase`, olisin joutunut muuttamaan sekä koodiini että testiini funktion nimen. Yleisestikin testejä tarvitsee aina muuttaa rakenteellisesti vähemmän, mikäli testaan toimintaa enkä toteutuksen yksityiskohtia.

Myönnettäköön, että tässä vertaus jo hieman ontuu. Todennäköisesti testien muokkaaminen jälkikäteen on hieman helpompaa kuin kiinnikkeiden paikkojen siirtäminen kallioseinämässä. Eikä siinäkään olisi tapahtunut mitään peruuttamatonta, vaikka funktion nimi olisi alunperin kuvannut toteutuksen yksityiskohtaa (`toUpperCase`) eikä toimintaa (`shout`). Olisin ihan näppärästi voinut muuttaa funktion nimen vasta siinä kohtaa, kun toiminnallisuus muuttuu. Käyttämämme työkalut ovat sentään sen verran näppäriä.

## Turvallisesti huipulle

Mitä sitten testit tarjoavat, jos ne eivät tuo esiin kuin ne virheet jotka jo tiedämme? Niistä kuulostaa olevan kauheasti vaivaa, varsinkin reitin muuttuessa. Kiipeiljä asettaa kallioseinämään kiinnikkeet, jotta eteneminen olisi turvallista. Tämä pätee yhtälailla sovelluskehitykseen. Testaus pitää muutosten aiheuttamat riskit kurissa.

Vaikka jokin virhe osattaisiin kuvitella etukäteen, on sen vakavuutta hankala ennustaa. Voi olla, että käyttäjänimessä oleva erikoismerkki estää käyttäjää saamasta sovellukselta mitään ilmoituksia, koska nimen muuttaminen isoiksi kirjaimiksi kaataa koko ilmoituksen muodostamisen. Tuo käyttäjä saattaa tuottaa suuren osan sovelluksen kautta saatavasta liikevaihdosta. Ehkä kilpailijan sovellus toimii paremmin? 
