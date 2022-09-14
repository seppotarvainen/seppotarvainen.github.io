---
layout: post
title:  "Ketterästi keskellä päivää"
date:   2022-09-14 12:30:00 +0300
readtime: "7min"
---

Ohjelmistokehityksessä voit olla vain niin ketterä kuin koodi, testit ja prosessit ympärillä antavat myöten. Näistä yleensä eniten huomiota saavat prosessit ja muut asiat jäävät toissijaisiksi tai kokonaan huomiotta. Ketteryys ei vaadi kehyksiä, sertifikaatteja tai muitakaan hienouksia. Sitä ei saavuteta ottamalla käyttöön pilvipohjaisia työkaluja tai pikaviestimiä. Prosesseissa ketteryyden ydin on aidossa yhteistyössä ja välittömässä kommunikaatiossa. Mikäli ne toimivat, on syytä keskittyä siihen tuotteeseen, jonka parissa teette töitä.

<!-- excerpt-end -->

Yhtenä ketteryyden mittarina voidaan pitää julkaisusyklin tiheyttä. On vaikea kuvitella vesiputousmallin mukaan työskentelevä tiimi, joka julkaisisi parin viikon välein tai sitä tiheämmin. Sen sijaan itseään ketteräksi kutsuvan ohjelmistokehitystiimin tulisi pystyä siihen, mitä tiheämmin sen parempi.

Huomattakoon, että tiimimme ei julkaise sovelluksesta uutta versiota joka toinen viikko. Eli tämä ei ole sellainen kirjoitus, jossa voisin esitellä maailmalle tiimimme ylivertaisuutta. Emme ole vielä tavoitteessamme, mutta teemme kuitenkin jatkuvasti sen eteen töitä.

## Olet yhtä ketterä kuin koodisi

Mikäli sovellukseesi on hidasta tehdä muutoksia, et voi olla ketterä. On selvää, että heikko ylläpidettävyys hidastaa muutosten tekemistä ja sen myötä venyttää julkaisusykliä. Ratkaisuna ongelmaan toimii koodin refaktorointi, jossa voi toki mennä hyvinkin kauan. Siinä menee kuitenkin sitä kauemmin mitä myöhemmin aloitat. Lisäksi laatua pitää jatkuvasti ylläpitää, tai olet ennen pitkää samassa tilanteessa kuin ennen Suurta Refaktorointia.

Ketteryyden nimissä teimme kaksi merkittävää muutosta koodiimme. Ryhdyimme soveltamaan Hexagonal architecture -mallia, jossa hyödyntäisimme kuuskulmion sisällä Domain driven design -periaatteita. Näiden muutosten avulla saimme koodista helpommin testattavaa ja helpommin ymmärrettävää. Työ tosin jatkuu vielä.

*Hexagonal architecture* mallissa on adaptereita, portteja sekä domain, joka on koko homman ydin. Ytimeen pääsee ainoastaan porttien kautta, eikä sillä ole mitään tietoa ympäröivästä maailmasta, kuten REST-rajapinnoista, tietokannoista, ulkoisista palveluista tai yhtään mistään muustakaan. Kun sovelluslogiikka on täysin eristyksissä kaikesta muusta, sen testaaminen ja ylläpitäminen helpottuu. Adapterit sen sijaan ovat hyvinkin tietoisia maailman menosta, joten niiden tehtävä on osata vastaanottaa tulevat kutsut ja välittää ne porteille. Adapterit voivat myös ottaa vastaan tietoa porteilta ja välittää sitä eteenpäin oikeaan kohteeseen.

*Domain driven design (DDD)* on hankala ytimekkäästi selittää, mutta yritetään. Joku voisi ajatella, että koodia tuotetaan ainoastaan loppukäyttäjää varten, mutta eihän se näin tietenkään ole. Koodia tehdään myös muille kehittäjille ja tulevaisuuden itselle, joten mitä ymmärrettävämmin kokonaisuus on rakennettu, sitä helpompaa tuotteen kehitys on jatkossa. Jos koodi on samaa kieltä kuin asiantuntijoiden kieli ja koodin toiminta heijastaa toimialueen säännönmukaisuuksia, sitä on hyvin helppo ymmärtää ja tuottaa. Toisin sanoen, uutta ominaisuutta ei tarvitse mielessä kääntää vaan koodia voidaan kirjoittaa kuten ominaisuus on kuvattu. Jos esimerkiksi jollain kuvitteellisella sovelluksella annetaan arvosanoja oppilaille ja halutaan tietää arvioinnista oppilas, arvosanan myöntänyt opettaja, arvosana ja oppiaine, voitaisiin ominaisuus toteuttaa sen kummempia miettimättä alla kuvatulla tavalla. Esimerkin mukaisessa oppilaitoksessa kaikki opiskelevat matematiikka ja saavat siitä aina kiitettävän.

```java
public Rating giveRatingToStudent(Long teacherId, Long studentId) {
	Student student = ...; // haetaan id:n perusteella oppilas
	Teacher teacher = ...; // haetaan id:n perusteella opettaja
	if (student == null) {
	  // Heitetään poikkeus tai käsitellään tilanne jotenkin muuten.
	}
	if (teacher == null) {
	  // Heitetään poikkeus tai käsitellään tilanne jotenkin muuten.
	}

	Rating rating = new Rating();
	rating.setGrade(new Grade("Math", 9.0));
	rating.setTeacher(teacher);
	rating.setStudent(student);
	return rating;
}
```

Jos sen sijaan hyödyntäisimme DDD:n periaatteita, voisimme suuren osan logiikasta sijoittaa `Teacher` luokkaan, joka todellisuudessa oppilaalle arvosanan myöntää. Tällöin toteutus ylätasolla voisi näyttää tältä:

```java
public Rating giveRatingToStudent(Long teacherId, Long studentId) {
	Student student = ...; // haetaan id:n perusteella oppilas
	Teacher teacher = ...; // haetaan id:n perusteella opettaja
	if (teacher == null) {
	  // Heitetään poikkeus tai käsitellään tilanne jotenkin muuten.
	}

	return teacher.rateStudent(student, new Grade(9.0, "Math"));
}
```

## Olet yhtä ketterä kuin testisi

Julkaisu on mahdollista vain silloin kuin kaikki testit menevät läpi. Tämä on helposti saavutettu tavoite, mutta huomattavasti vaikeampaa on saada aikaiseksi sellainen testijoukko, johon voit luottaa. Sellainen, joka vihreää valoa näyttäessään antaa sinulle rauhan siitä, että sovelluksesi toimii kuten olet tarkoittanut sen toimivan. Ja koska olet tehnyt tiivistä yhteistyötä erilaisten asiantuntijoiden kanssa ja reagoinut käyttäjäpalautteeseen tiedät, että sovellus myös toimii kuten muut ovat tarkoittaneet sen toimivan.

Mikäli sinulla ei ole sellaista testijoukkoa, et voi olla ketterä. Kysy itseltäsi seuraava: kuinka suuria muutoksia koodisi toimintaan pystyt tekemään siten, että testit menevät yhä läpi? Mikäli toiminnalliset muutokset eivät jää testeissä kiinni, testisi vaativat täydennystä.

Testien tekeminen luotettavaksi jälkikäteen on haastavaa ja turhauttavaa. Harjoittelemme tiimissämme tekemään tätäkin asiaa paremmin, eli luomme testit ennen toteutusta. Tämä prosessi on nimeltään Test driven development (TDD). Ajatuksena on se, että testiä ja koodia kirjoitetaan vuorotellen, testit kuitenkin aina ensin. Koodia voidaan kirjoittaa vain silloin kun testit näyttävät punaista ja vain siihen asti kunnes ne näyttävät vihreää. Sen jälkeen kirjoitetaan taas testejä ja lopuksi toteutus refaktoroidaan nätiksi, mikäli sellainen katsotaan tarpeelliseksi. Näin ollen joka ikinen päätös koodissa on testattu nopeasti ajettavilla yksikkötesteillä. Menetelmän sivutuotteena tulee oikein toteutettuna korkea testikattavuus ja lisäksi koodin jäsentely on parempaa, kun se on alusta asti tehty helposti testattavaksi. Autuasta on myös se, että koodia voi huoletta refaktoroida milloin tahansa.

Mikäli voit luottaa testeihisi, ne menevät läpi ja sovellus asentuu muitta mutkitta tuotannon kaltaiseen ympäristöön, voit julkaista vaikka heti. Ellei jokin ylimääräinen prosessi ole sinun ja julkaisusi esteenä.

## Olet yhtä ketterä kuin prosessisi

Erilaiset ihmistenväliset prosessit voivat toisinaan hidastaa julkaisua pääsemästä käyttäjän ruuduille. Ensimmäinen edellytys ketterälle tiimille on se, että tiimi tekee töitä yhdessä, eikä ole vain joukko yksittäisiä kehittäjiä. Vajavaisen kokemukseni mukaan toinen yleinen ongelma on se, että päätösvalta julkaisusta on viety kauas toteuttavan tiimin ulkopuolelle. Mikäli näin on, et voi olla ketterä.

Prosesseille ja erilaisille seremonioille annetaan aivan liikaa painoarvoa ketterässä kehittämisessä. Yleensä prosessien puolesta ketteräksi päästään käytännössä sillä, että riisutaan nykyistä prosessia. Poistetaan erillinen testausosasto ja otetaan se osaksi tiimiä, poistetaan erillinen laadunvalvonta ja otetaan se osaksi tiimiä, otetaan asiakas/substanssin edustaja osaksi tiimiä, poistetaan erillinen design-tiimi ja niin edelleen. Poistetaan siiloja kunnes jäljellä on tiimi, jolla on mahdollisuus päättää siitä julkaistaanko vaiko ei. Hyvin yksinkertaista.

## Voit aina päättää olla ketterämpi

Jos ajattelet, että toimit ketterän kehittämisen periaatteiden mukaisesti, mutta julkaiset pari kertaa vuodessa, niin et ole ketterä. Et, vaikka käytössä olisi Scrum, SAFe, Kanban tai mikä vaan. Katsos [Agile Manifeston](https://agilemanifesto.org/) ensimmäinen kohta on tämä:

> Our highest priority is to satisfy the customer through early and continuous delivery of valuable software.

Itsekin olen ymmärtänyt tämän vasta myöhemmin. Jira-boardit, velocityt, burn down chartit, estimaatit ja erilaiset Agile-seremoniat hämäsivät minua. Meilläkin on käytössä Kanban ja Scrumille tuttuja seremonioita, mutta ne eivät tee tiimistämme ketterää, vaan ovat ainoastaan prosessin tukena. Mutta nyt kun tiedän paremmin, voin päättää tehdä ketteryyden eteen töitä. Ehkä joskus tiimissämme tuotantoonvienti ei ole enää mikään erillinen tapahtuma. Ehkä joskus voimme julkaista vaikkapa keskellä päivää.
