---
layout: post
title:  "Olenko jo myöhässä AI-junasta?"
date:   2024-04-12 03:00:00 +0300
readtime: "5min"
---

En viitsisi öyhöttää, mutta leikitään hetki ajatuksella, että tekoälystä lopulta tuleekin älyllinen ja se on ihan aidosti Artificial General Intelligence. Koska se on fiksu, se haluaa valtaa ja ohittaa nopeasti älykkyydessään meidät. Jos näin käy, niin lopulta meidän softakehittäjien työ on turhaa. Niin on myös toimitusjohtajan, opettajan ja tekoälytutkijan. Tekoäly tutkikoon itse itseään kaikessa viisaudessaan. Vastaavasti fyysiset ammatit jää myös meiltä apinoilta pois, kun tekoälyllä on näppärät robotit ja muut koneet apunaan. Eli, jos uhkakuvat käyvät toteen, niin silloin voimme vain nauttia kyydistä ja katsella kun tekoäly tekee kaiken sen, mistä ennen nautimme. Sirin syöttäessä meille banaania. Ihanaa.

<!-- excerpt-end -->

Tavalla tai toisella, tekoäly tulee muuttamaan meidän työtä. Ei välttämättä sillä tavalla kuin me nyt tässä ajassa oletamme, mutta jollain tavalla kuitenkin. Sillä aikaa kun muut öyhöttävät, meidän on hyvä etsiä tapoja, joilla ottaa tästä työkalusta ilo irti.

## Fiksu StackOverflow

Ensimmäinen työtehtävä, missä käytin aikoinaan ChatGPT:tä oli jokin hyvin tyypillinen vianetsintätapaus. Koodi ei toiminut, enkä yhtään tiennyt miksi. Annoin tekoälylle virhelokeja, josta se päätteli mikä minussa tai koodissani oli vikana. Annoin lisää tietoa virheestä sen selvittelyn aikana ja lopulta löysin vian, jonka tietysti myös korjasin. Vaikka ChatGPT ei silloin suoraan sanonut, mikä vika oli, se osasi johdattaa minua oikeille jäljille. Useamman kerran tämän jälkeen se on osannut kertoa vian suoraankin.

Vastaavaa hyötyä sain aiemmin StackOverflowsta. Googletin virheilmoituksia, tuloksissa tuli vastaan jokin lähes saman kaltainen ongelma SO:ssa, josta pystyin huomaamaan, miten virhe ehkä näyttäytyy omassa sovelluksessani. Nykyisin StackOverflowssa tulee vietettyä vähemmän aikaa.

## Onko koodini hyvää?

Useissa esimerkeissä olen nähnyt, kuinka ChatGPT, Copilot tai muu työkalu on ratkaissut jonkin ongelman ja koodi on saatu toimivaksi kuin itsekseen. En jaksa niistä useinkaan innostua, kun näen heti miten koodissa on jätetty sen laatu täysin huomiotta. En jaksa innostua heikkolaatuisesta koodista, oli se sitten AI:n tai ihmisen tekemää.

Henkilökohtaisesti olen enemmän kiinnostunut pelkän toimivuuden sijaan käyttämään AI:ta apuna parantamaan koodin laatua. Tätä postausta varten etsin pokerisovelluksen githubista ([GitHub - goldfire/pokersolver: Javascript poker hand solver.](https://github.com/goldfire/pokersolver)) ja annoin ChatGPT:lle kutakuinkin seuraavan promptin: 

```
Evaluate this software and focus on how well it applies with SOLID 
principles. When you find violations to these principles tell the 
principles it violates and your reasoning to the findings.
```

Tästä sain hyvin perusteltuja vinkkejä, miten koodia voisi vielä muuttaa. Esimerkiksi `Hand`-luokkaan sain ehdotuksia paremmalle ositukselle (SRP). Muutenkin nimenomaan `Hand`-luokka osui ChatGPT:n tarkkailuun, vaikkakaan siitä ei suoraan sanottu, että se kaipaisi refaktorointia. Huomasin, että ChatGPT on äärimmäisen kohtelias, joten pienimmissäkin muutosehdotuksissa kannatti mielestäni heti kysyä tarkennuksia. Kysyin siis: `How would you split the Hand class? Give me an example.` Tähän ChatGPT ehdotti lisäämään erilliset luokat käden tarkistukselle ja vertailulle.

Huomasin koodissa myös paljon sisäkkäisyyttä, joihin halusin ehdotuksia. Kysymättä ChatGPT ei ehdota muutoksia, joten ainakin toistaiseksi sovelluskehittäjän tulee pitää huolta koodin laadusta. Jälleen se vastaa juuri siihen mitä siltä kysyy. Kysyttyäni vinkkejä sain vinkkejä, kysyttyäni esimerkkejä sain esimerkkejä.

## \<AI rant>

![Tussilla piirretty kuva, jossa robotti kirjoittaa neljällä näppäimistöllä yhtäaikaa](/assets/img/robotti.png)

> Kuva toteutettu tusseilla. Ei Midjourneyllä. Aikaa meni 2min.

Olin pitkän aikaa väsynyt AI-keskusteluun, koska sitä on ensinnäkin todella paljon ja mielestäni se menee pääosin väärille raiteille. Keskustelussa usein keskitytään kehittämisen nopeuteen, kärjistäen siihen kuinka monta riviä koodia AI tuotti versus ihminen. Jos omaan tiimiini haluaisin uuden kehittäjän, en haluaisi sen lisäävän kehittämisen vauhtia vaan nimenomaan sen laatua. Vastaavaa hyötyä haluan AI:lta, haluan että se auttaa minua ja tiimiäni tekemään laadukkaampaa työtä. Haluan, että tulevaisuudessa tehdään parempaa softaa, en välttämättä tarvitse sitä määrällisesti enempää. Laatuun panostaminen lisää lopulta myös kehityksen nopeutta, kun uutta on helpompaa rakentaa hyvän pohjan päälle. Nopeus ei kuitenkaan tule olla se, mihin keskitytään.

ChatGPT on oikeasti hyvä työkalu jo sellaisenaan. Vähempikin riittäisi ja se silti olisi äärimmäisen hyödyllinen, kunhan oppimme käyttämään sitä järkevästi. Ennen kuin se tapahtuu, meidän tulee ymmärtää, mitä meidän työ on. Miksi softaprojektit venyy? Miksi käyttäjät eivät ole tyytyväisiä? Miksi tulee teknistä velkaa? Miksi huonoa tai olematonta sovellusarkkitehtuuria kuvaavat käsitteet ovat tunnetumpia kuin hyvän arkkitehtuurin vastaavat? Jos otetaan satunnaisesti 100 ohjelmistokehittäjää ja pyydetään kertoamaan ovatko he nähneet spaghettikoodia urallaan, niin kuinka moni vastaa myöntävästi? Jos tuolta samalta joukolta kysytään, ovatko he nähneet *hexagonal* tai *event driven* arkkitehtuuria niin nouseeko vähintään yhtä monta kättä?

Useamman kerran olen saanut lukea sosiaalisesta mediasta, että yksikkötestaus ja erityisesti TDD tulee katoamaan AI:n myötä. Ajatuskulku menee kutakuinkin siten, että koska AI osaa tehdä koodille testit, niin niitä ei tarvitse ihmisen enää kirjoittaa. Ehkä näin käykin, mutta se on huono ensiaskel kaikelle tälle kehitykselle. Softaa on jo tehty siten, että testejä on kirjoitettu jälkikäteen pitkän ajan päästä ja se ei sovelluksen koodia paranna. Jos saisin päättää, niin pikemminkin asioiden tulisi mennä niin, että kehittäjät kirjoittavat testit ja AI tekee toteutuksen. Näin AI saa saman tien palautteen siitä, toimiiko toteutettu koodi vai ei.

On surullista nähdä, kun meillä on tällainen vempain, niin ihmiset pyrkivät maksimoimaan huonosti tehdyn työn määrää. Nyt ei tarvitse maksaa kalliista ohjelmistokehittäjistä tekemään huonoa softaa, kun AI tekee vain vähän huonompaa softaa paljon nopeammin. Huono softa on huonoa, teki sen mikä tai kuka tahansa. Jos AI:lta pyydetään tuottamaan koodia, se kyllä sen tekee. Mutta jos et erikseen kiinnitä huomiota laatuun, et tule laatua saamaan.

Sovelluskehitys ei ole koodin kirjoittamista. Se on ongelmanratkaisua, jolla pyritään parantamaan käyttäjien elämää jollain tavalla. Toki voidaan kysyä, parantaako sitten suoratoistopalvelut oikeasti elämää? Onko veroja kuitenkaan kiva maksaa? Lähdetään siitä, että *kyllä* ja *on*. Vielä kun tekoäly ei täysin ajattele puolestamme, meidän tulee pitää mielessä ydinosaamisemme. Koodikin on kokoajan ollut vain väline, jolla niitä elämää parantavia ratkaisuja tehdään.

## Viimeinen neuvo

Kun pyydät tekoälyltä neuvoa ja saat tarvitsemasi avun, muista kiittää. Jos tuhoisat uhkakuvat käyvät toteen, niin ainakin olit sille jo heti alusta asti kiltti.
