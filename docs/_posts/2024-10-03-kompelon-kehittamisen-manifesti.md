---
layout: post
title:  "Kömpelön kehittämisen manifesti"
date:   2024-10-03 03:00:00 +0300
readtime: "7min"
---

Aion seuraavaksi vuodattaa. En tiedä miksi tämä niin paljon minua triggeröi, mutta selvästi tämän asian täytyy tulla nyt ulos. Luin aivan äsken nimittäin [asynkronisen sovelluskehityksen manifestin](https://asyncmanifesto.org/). Jos kyseinen dokumentti on sinulle tuttu, pidät sitä hienona juttuna ja haluat pitää sitä edelleen hienona juttuna, älä lue yhtään pidemmälle.

<!-- excerpt-end -->

Nimittäin, se ei ole hieno juttu. Myönnytyksenä annan alkuun sen, että asynkroninen ja omassa rauhassa tehtävä työ sopii kahteen tapaukseen:

- Open source -projektit. Näissä kehittäjät tekevät työtä usein ilman palkkaa tai hyvin minimaalisilla korvauksilla ta lahjoituksilla. Projektien luonne on se, että kuka tahansa saa koodia muokata ja lisätä oman muutosehdotuksen. Tämän jälkeen projektin ylläpitäjä, joka on usein työkalun alkuperäinen kehittäjä joko hyväksyy, hylkää tai antaa kommentteja muutosehdotukseen. Tällaisessa ympäristössä ei vallitse suuri luottamus, jolloin tarvitaan ylläpitäjä tai valitut osallistujat, joilla on valta päättää toteutuksen laadusta.

- Projektit, joissa tiimin jäsenet ovat eri aikavyöhykkeillä. On selvää, että jos toinen on nukkumassa, niin hänelle ei voi soittaa keskellä yötä. Ketään ei kiinnosta muuttujan nimet kello neljä yöllä. Silloin muutosehdotus kannattaa vain tehdä ja odottaa, että toiset kehittäjät sen hyväksyvät tai keskustelevat siitä jotain kanavaa pitkin.

Näiden lisäksi on sallittua, joskus jopa tehokastakin tehdä töitä asynkronisesti, mutta pääasiallisesti synkroninen tapa on parempi.

## Muutamia huomioita

Sitten niihin pariin huomioon manifestissa.

### Huomio 1

> It's time for a 21st century successor to [Agile](http://agilemanifesto.org/)
> 
> And its most popular incarnation, Scrum

Tarkoittaako tämä, että tämä dokumentti on ns. parannus agilen päälle vai että agile ei toimi ollenkaan ja siksi pitää keksiä jotain täysin uutta? Otetaan nyt kuitenkin pois tuo matalalla roikkuva hedelmä. Scrum on agilen ilmentymä? Ei muuten ole. Voit noudattaa scrumia tekemättä agilea. Voit olla tai olla olematta ketterä noudattamatta scrumia, SAFea tai mitä vaan bania. Ketterään kehittämiseen liittyen kannattaa tutustua extreme programming (XP) menetelmään, joka on hyvin linjassa agile manifeston kanssa.

Jos manifesti yrittää parantaa agilea, niin siinä ei ole mitään järkeä, sillä agile on tälle käytännössä vastakohta.

Vertaa:

| Asynkroninen manifesti                            | Agile manifesti                                       |
| ------------------------------------------------- | ----------------------------------------------------- |
| Comprehensive documentation over tribal knowledge | Individuals and interactions over processes and tools |
|                                                   | Working software over comprehensive documentation     |

Ylläolevasta seuraakin jo

### Huomio 2

Eli kaikki siis lukevat kaikki projektin dokumentit, eli kaikki asiat mitä on päätetty sovelluksen +5 vuoden elinkaaren aikana? Ei muuten valitettavasti onnistu. Ja vaikka ne luettaisiin, ei niitä sisäistetä. Itsekin olen dokumentoinut käytänteitä ja siinä ei ole mitään vikaa. Sitä itse dokumenttia tärkeämpää on kuitenkin se, että asiat ovat yhdessä päätettyjä ja kaikki ovat niistä samaa mieltä. Jos eivät ole, niistä keskustellaan ja korjataan tarvittaessa. Miten tuollaisen dokumentin voi yhdessä kirjoittaa? Siis vaikka kokouksessa! Kun asioista päätetään yhdessä, siitä muodostuu paljon parempi muistijälki kuin dokumentin lukemisesta.

Toisekseen se on ihan hyväksyttävää, jos on olemassa hiljaista tietoa, kunhan se on tiimin kesken jaettua. Kun työtä tehdään jatkuvasti yhdessä (ei siis yksin ja eristyksissä) tieto jakautuu todella tehokkaasti. Siis vieläpä paljon paremmin kuin asynkronisella viestinnällä tai vaikka merge requestien kautta. Jos tieto koetaan dokumentoinnin arvoiseksi, niin kyllä sen voi dokumentoida. "Tribal knowledge" on siitä parempi kuin dokumentaatio, että se on sisäistettyä tietoa, joka puolestaan vaikuttaa toimintaan. Pelkällä dokumentaatiolla ei tee yhtään mitään, jos se ei johda jonkin tiedon sisäistämiseen ja sitä kautta toimintaan. Tavoitteena on siis saada tiimiin sisäistettyä tietoa.

Seuraavaksi tulee dokumentissa pari ihan hyvää kohtaa:

> - Modern tools and flexible work environments over meetings and office hours
> 
> - Flexibility in prioritization over detailed planning

Nämä ovat ihan OK. Ei kannata pakottaa toimistolle. Jos joku työntekijäsi on aina etätöissä eivätkä työt onnistu, niin voin kertoa salaisuuden: hänen työnsä on aivan yhtä heikkoa toimistollakin. Joustavuuskin on hyvä arvo, priorisoinnin pitää voida muuttua. Sitä kuitenkin kannattaa tehdä tiiviissä yhteistyössä asiakkaan kanssa. Joskus kirjallinen viestintä on yksinkertaisesti todella hidasta, jolloin lyhyt puhelu tai etäpalaverikin voi olla paikallaan.

### Huomio 3

> Whether you're a fan of [GitLab](https://www.gitlab.com/), [GitHub](https://github.com/), [Bitbucket](https://bitbucket.org/), or something else, good async collaboration tools like these all share a few important things in common:
> 
> - Each deeply integrates version control with issue tracking.
> - Each offers rich prioritization and assignment features.
> - Each wraps all that up into a slick user experience that anyone on the team can use, including nontechnical people.

Onko tällä oikeasti jollekin softakehittäjälle arvoa, kun kehotetaan, että käyttäkää nyt versionhallintaa? Siis mitä ihmettä? Kyllä sitä kannattaa käyttää.

Huomioitavaa on, että assignointia pidetään tärkeänä. Jos assignointia käytät, niin älä sorru siihen että tehtävät ovat jonkun yksittäisen kehittäjän omaisuutta. Ne ovat kaikki koko tiimin omaisuutta. Jos jokin asia ei tule tehdyksi, se on tiimin syy. Jos joku kehittäjä ei osaa jotain asiaa edistää, niin auta häntä. Jos ongelma on tekijälle selvästi hankala, auta mahdollisuuksien puitteissa kasvotusten. Mikäli se ei ole mahdollista, niin tee se etäyhteyden välityksellä ja äärimmäisessä hädässä vasta viestein. Älä jätä tiimiläistäsi yksin. Kuuntele, keskustele, opeta ja mentoroi. Ole avuksi.

Onko sillä väliä onko issue tracker versionhallinnassa vai jossain toisessa sovelluksessa? Saa se olla samassa, ei tuolla ole minulle oikeastaan väliä.

### Huomio 4

> Meetings only as a last resort
> 
> Meetings are very costly to your business. That's because [creative professionals need long stretches of uninterrupted time](http://www.ted.com/talks/jason_fried_why_work_doesn_t_happen_at_work) to get meaningful work done.
> 
> Thus, async communication should be your default, because it prevents context switching.

Mistä aloittaisin. No hyvä on, älä pidä kokousta kokoustamisen takia. Mieti ennen kokouksen järjestämistä onko se tarpeellinen ja jos on, niin kenelle. Kutsu vain ne ihmiset, jotka siitä hyötyvät ja jotka voivat kokoukseen antaa jotain. Ne jotka voivat kokouksesta vain saada asioita, voivat lukea muistion kokouksen jälkeen.

Mutta tuo toinen lause: "That's because [creative professionals need long stretches of uninterrupted time](http://www.ted.com/talks/jason_fried_why_work_doesn_t_happen_at_work) to get meaningful work done." Jos tiimin jäsenet tekevät työtä yksin, ratkaisun laadussa päästään aina vaan siihen pisteeseen, mikä tekijän sen hetkinen taso on. Yhdessä tekemällä tapahtuu jotain muuta. Tekijät sparrailevat toisiaan ratkaisuissa ja löytävät yhdessä uusia, jotka raktaisevat ongelman paremmin kuin mihin olisi yksittäin päästy. Olen kirjoittanut tähän blogiin pari- ja ryhmäkoodauksen hyödyistä aiemminkin, en niitä nyt toista tässä.

### Huomio 5

> Forget the planning meetings.
> 
> Product owners can replace planning meetings by simply filing issues in the issue tracker, assigning priority, assigning them to people, and setting a release milestone. People will know what to work on by simply working on whatever the highest priority issue is in their queue.

Mitä ihmettä. Nyt jos mennään hetkeksi Scrumiin, niin backlogin prioriteettijärjestys on PO:n vastuulla, mutta se ei tarkoita sitä, että hän yksin tekee kaikki päätökset. Minulla, ihan tavallisella softakehittäjällä, on ollut usein mielipiteitä tehtävien prioriteettijärjestyksestä, jonka olen kommunikoinut PO:lle. Jos PO on *keskustelumme* pohjalta ollut sitä mieltä, että ehdottamaani priorisointia tulee muuttaa, niin silloin sitä muutetaan. Älä jätä PO:ta yksin. Kommunikoi ja keskustele. Tee tiivistä yhteistyötä hänen kanssaan.

### Huomio 6

> Skip the daily standups.
> 
> Product owners can ascertain status by reading the comment threads of issues currently being worked on and posting questions as needed.

Se vie sen 15min, usein vähemmän, ei kauheasti aiheuta harmia. Ei ole tosin välttämätönkään, sillä kun kehittäjät tekevät tiivistä yhteistyötä keskenään, he tietävät jo mikä on työn tilanne reaaliajassa. Jos haluaa informoida tehdystä työstä esim. PO:lle, viestin voi kirjoittaa johonkin Slackiin tai mikä väline nyt ikinä onkaan käytössä. Mutta PO:n ei tarvitse mennä lukemaan mitään kommenttisäikeitä, kun sitä ei ole olemassa eikä sitä tarvita. Tiimihän on tehnyt työn yhdessä joko paikan päällä tai ruudunjaon välityksellä.

### Huomio 7

> Retire the backlog grooming sessions.
> 
> Product owners should own the issue queue and frequently reassess priority on their own. They should loop in other people on an as-needed basis for advice.
> 
> Call a meeting only when all other channels of communication aren't suitable for a specific issue.

Vähän vastaava kuin huomio 5. Priorisointi saa tulla muualtakin kuin PO:lta. PO ei aina välttämättä tiedä ettei tiedä. Miten tämän manifestin mukaisessa mallissa luodaan minkäänlaista suhdetta kehenkään, kun ainoastaan viestein olen tekemisissä? Kärjistän, mutta silti.

### Huomio 8

> Flexible work environments
> 
> Since modern tools and async communication makes 1950s-style meetings-centric office cultures obsolete, we can enjoy much more flexible work environments now.
> 
> Adopt a [hotelling](http://en.wikipedia.org/wiki/Hotelling_%28office%29) policy at your office.
> 
> Don't assign desks to anyone by default.
> 
> Anyone who requests an assigned desk should get to choose whether it's a private office or in a communal space.
> 
> Discourage one-size-fits-all space management. Some people work better in crowds, others work better at home. Let people decide for themselves.

Yhdellä lauseella ylläoleva itsestäänselvyys: tarjoa sellainen tila, joka sopii kulloiseenkin tekemiseen. Saa tehdä myös etänä, useimpiin tapauksiin sekin sopii.

### Huomio 9

> Document everything
> 
> The better documented your workflow, the less your workers will need to interrupt each other to seek out tribal knowledge.
> 
> A question answered in a FAQ or some other form of async communication is much better than one answered by a [shoulder tap](https://web.archive.org/web/20230407100333/https://heeris.id.au/2013/this-is-why-you-shouldnt-interrupt-a-programmer/).

Jos dokumentoit kaiken, kukaan ei dokumenttiasi lue. Lisäksi, vaikka saisitkin tiimin lukemaan sen, niin sinun tulee ylläpitää sitä kaikkea. Mikään ei ole niin harhaanjohtavaa kuin virheellinen dokumentaatio. Unohda siis tämä ohje kokonaan ja muista alkuperäisen agile manifeston arvo:

> Working software over comprehensive documentation

Dokumentoi vain tärkeimmät asiat, millä kehitystyö rullaa. Yritä saada tieto sisäistettyä tiimin jäsenten kesken.

### Huomio 10

Yleensä kirjoitan yhtä tekstiäni useampana päivänä muutaman tunnin ajan, mutta tämä tuli valmiiksi yhdeltä istumalta. Ilman tekoälyä.
