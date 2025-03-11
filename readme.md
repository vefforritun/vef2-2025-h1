# Vefforritun 2, 2025, hópverkefni 1

[Kynning í fyrirlestri](https://youtu.be/abHe9ADi2VI?t=547).

## Verkefnið

Útbúa skal vefþjónustur fyrir verkefni ákveðið af hópnum. Þetta er ólíkt hópverkefnum seinustu ára þar sem vel skilgreindar vefþjónustur hafa verið gefnar til útfærslu. Hægt er að fá tilfinningu fyrir útfærslu með að skoða sýnilausnir á þeim verkefnum:

- [Hópverkefni 1 árið 2022 (matsölustaður)](https://github.com/vefforritun/vef2-2022-h1) og [sýnilausn á því](https://github.com/vefforritun/vef2-2022-h1-synilausn).
- [Hópverkefni 1 árið 2021 (sjónvarpsþættir)](https://github.com/vefforritun/vef2-2021-h1) og [sýnilausn á því](https://github.com/vefforritun/vef2-2021-h1-synilausn).
- [Hópverkefni 1 árið 2019 (vefverslun)](https://github.com/vefforritun/vef2-2019-h1) og [sýnilausn á því](https://github.com/vefforritun/vef2-2019-h1-synilausn).
- [Hópverkefni 1 árið 2018 (bókasafn)](https://github.com/vefforritun/vef2-2018-h1) og [sýnilausn á því](https://github.com/vefforritun/vef2-2018-h1-synilausn).

Verkefnið er metið út frá kröfulýsingu sem gefin er og samanstendur af bæði [_functional_](https://en.wikipedia.org/wiki/Functional_requirement) og [_non-functional_](https://en.wikipedia.org/wiki/Non-functional_requirement) kröfum fyrir verkefnið.

## Kröfulýsing

### Gagnagrunnur og gögn

Nota skal postgres gagnagrunn og setja upp a.m.k. sex töflur sem tengjast á einhvern máta.

Nota skal viðeigandi virkni til að merkja dálka, t.d.

- Setja sem auðkenni (`primary key`).
- Merkja tengingar (`foreign key`).
- Merkja sem einstakt (`unique`).
- Merkja reiti sem viðeigandi gagnatag (strengir, tölur, dagsetningar, texti).
- Setja viðeigandi lengd á reiti.

Í gagnagrunninn skal hlaða inn viðeigandi gögnum fyrir verkefnið, a.m.k. 50 færslur í heildina.

Nota má beinar SQL fyrirspurnir eða tól eins og [prisma](https://www.prisma.io/).

Hægt er að útbúa testgögn eða nota þjónustu eins og [faker](https://github.com/faker-js/faker).

Ef verkefni 2 eða 3 var hýst á Render getur verið að ekki sé hægt að útbúa annan gagnagrunn, þá er hægt að nota aðra hýsingu eða sérstaka gagnagrunnshýsingu, t.d. [Neon](https://neon.tech/).

### Vefþjónustur

Útfæra skal REST vefþjónustur til að útfæra alla virkni í verkefninu.

Huga skal að hönnun og uppsetningu á vefþjónustum:

- Staðfesta (validation) þarf og hreinsa öll gögn (sanitization) sem send eru inn af notendum, bæði óauðkenndum og stjórnendum.
- Nota skal `JSON` í öllum samskiptum.
- GET á `/` skal skila lista af öllum slóðum í mögulegar aðgerðir.
- Ef beðið er um eitthvað sem ekki er til skal skila `404`.
- Ef beðið er um einingu eða reynt að framkvæma aðgerð sem ekki er leyfi fyrir skal skila `401`.
- Allar niðurstöður sem geta skilað mörgum færslum (fleiri en 10) skulu skila _síðum_.
- Ef villur koma upp skal skila `400` með viðeigandi villuskilaboðum.
- Huga að samræmi á heitum, slóðum og villuskilaboðum.

## Notendaumsjón

Setja skal upp notendaumsjón sem skiptist a.m.k. í tvennt: óauðkenndur notandi og stjórnandi. Geyma skal a.m.k. fyrir hvern notanda:

- Auðkenni, t.d. netfang eða notendanafn.
- Lykilorð, geymt á öruggan máta.
- Staða, hvort notandi eða stjórnandi.

Óauðkenndur notandi getur skoðað einhver gögn og framkvæmt a.m.k. eina aðgerð.

Stjórnendur geta breytt, bætt við, og eytt efni (_CRUD_ aðgerðir.)

Nota skal JWT token og geyma notendur i gagnagrunni. Útfæra þarf auðkenningu, nýskráningu notanda og middleware sem passar upp á heimildir stjórnenda.

Útbúa skal í byrjun einn stjórnanda með notandanafn `admin` og þekkt lykilorð, skrá skal lykilorð í `README` verkefnis.

Ekki þarf að útfæra:

- Staðfestingu á netfangi.
- „Týnt lykilorð“ virkni.

### Myndastuðningur

Allar myndir skal geyma í [Cloudinary](https://cloudinary.com/) eða [imgix](https://imgix.com/), bæði þær sem settar eru upp í byrjun og þær sem sendar eru inn gegnum vefþjónustu.

Aðeins ætti að leyfa myndir af eftirfarandi tegundum (`mime type`):

- jpg, `image/jpeg`
- png, `image/png`

Aukalega eða í staðinn fyrir myndastuðning er líka hægt að setja upp vídeó stuðning með [Mux](https://www.mux.com/).

### Tæki, tól og test

Nota má Express, Hono eða önnur framework fyrir vefþjónustur, berið önnur framework undir Óla áður en lagt er af stað.

Setja skal upp eslint fyrir JavaScript. Engar villur skulu koma fram ef npm run lint er keyrt. Leyfilegt er að skilgreina hvaða reglusett er notað, ekki er krafa um að nota það sem hefur verið notað í öðrum verkefnum.

Setja skal upp jest til að skrifa test. Skrifa skal test fyrir a.m.k.:

- fjóra endapunkta, þar sem
- a.m.k. einn krefst auðkenningar
- a.m.k. einn tekur við gögnum

Í `README` skal tiltaka hvernig test eru keyrð.

### Öryggi

Almennt skal huga að öryggi m.t.t. OWASP top 10. Þetta á sérstaklega við notendaumsjón og þegar tekið er við gögnum.

### Hýsing

Setja skal upp vefinn á Render, Railway eða Heroku (ath að uppsetning á Heroku mun kosta) tengt við GitHub með postgres settu upp.

## Hugmyndir

### Viðburðakerfi

Vinna áfram með verkefni 2 og [hópverkefni 2 úr vef1 2022](https://github.com/vefforritun/vef1-2022-h2) með því að útbúa viðburðakerfi sem leyfir skráningu á viðburðum og birtingu þeirra.

### Minnislistakerfi

Vinna áfram með [hópverkefni 2 úr vef1 2021](https://github.com/vefforritun/vef1-2021-h2) og útbúa minnislistakerfi.

### Myndbandavefskerfi

Vinna áfram með [hópverkefni 2 úr vef1 2020](https://github.com/vefforritun/vef1-2020-h2) og útbúa myndbandavef.

### README

Í rót verkefnis skal vera `README.md` skjal sem tilgreinir:

- Upplýsingar um hvernig setja skuli upp verkefnið.
- Öll route í vefþjónustu og viðkomandi aðgerð, þetta getur verið afrit af því sem `GET /` skilar, sjá að ofan.
- Dæmi um köll í vefþjónustu m.v. test gögn.
- Innskráning fyrir `admin` stjórnanda ásamt lykilorði.
- Nöfn og notendanöfn allra í hóp.

Mikilvægt er að einhvern veginn séu allar slóðir vefþjónustu tilteknar fyrir yfirferð.

## Hópavinna

Verkefnið skal unnið í hóp, helst með þremur einstaklingum. Hópar með tveim eða fjórum einstaklingum eru einnig í lagi, ekki er dregið úr kröfum fyrir færri í hóp en gerðar eru auknar kröfur ef fleiri en þrír einstaklingar eru í hóp.

Hægt er að auglýsa eftir hóp á slack á rásinni `#vef2-2025-vantar-hóp`.

Hafið samband við kennara ef ekki tekst eða ekki er mögulegt að vinna í hóp.

Í hópverkefni 2 verður unninn framendi ofan á þessar vefþjónustur og því getur verið gott að halda áfram í sama hóp. Það er hinsvegar ekki krafa og hægt að skipta um hóp, mynda nýjan eða hugsanlega vinna sem einstaklingsverkefni.

Notast skal við Git og GitHub. Engar zip skrár með kóða ættu að ganga á milli í hópavinnu, heldur á að „committa“ allan kóða og vinna gegnum Git.

Sjást ætti á commit history að allir meðlimir hóps hafi tekið þátt í verkefni.

Útbúa ætti a.m.k. fimm Pull Request (PR) þar sem búið er að fara yfir af öðrum meðlim í hóp.

## Mat

- 25% Gagnagrunnur og gögn.
- 30% Vefþjónustur.
- 15% Notendumsjón.
- 10% Myndastuðningur.
- 10% Tæki, tól og test. `README` uppsett, verkefni keyrir í hýsingu.
- 10% Hópavinna með Git og GitHub PR.

## Sett fyrir

Verkefni sett fyrir eftir fyrirlestur miðvikudaginn 5. febrúar 2025 og kynnt í fyrirlestri 12. febrúar.

## Skil

Tilnefna skal hópstjóra sem skráir sig í ákveðinn hóp undir „Hópverkefni 1“ í Canvas. Aðrir nemendur skrá sig í framhaldinu í sama hóp, hópstjóri getur líka skráð aðra nemendur í hópinn.

Útbúa skal hóp jafnvel ef verkefnið er unnið sem einstaklingsverkefni.

Hópstjóri skal skila fyrir hönd allra í Canvas í seinasta lagi föstudaginn 7. mars 2025.

**Mikilvægt er að öll skil séu gerð í hóp annars munu ekki allir nemendur fá einkunn.**

Skil skulu innihalda:

- GitHub notendanöfn allra (passa þarf að allir nemendur séu í hópnum!)
- Slóð á verkefnið keyrandi í hýsingu
- Slóð á GitHub repo fyrir verkefni. Dæmatímakennurum skal hafa verið boðið í repo. Notendanöfn þeirra eru:
  - `osk`
  - `ofurtumi`
  - `tomasblaer`

## Einkunn

Leyfilegt er að ræða, og vinna saman að verkefni en **skrifið ykkar eigin lausn**. Ef tvær eða fleiri lausnir eru mjög líkar þarf að færa rök fyrir því, annars munu allir hlutaðeigandi hugsanlega fá 0 fyrir verkefnið.

Ef stórt mállíkan (LLM, „gervigreind“, t.d. ChatGTP) er notað til að skrifa part af lausn skal taka það fram. [Sjá nánar á upplýsingasíða um gervigreind hjá HÍ](https://gervigreind.hi.is/).

Sett verða fyrir ([sjá nánar í kynningu á áfanga](https://github.com/vefforritun/vef2-2025/blob/main/namsefni/01.kynning/1.kynning.md)):

- fimm minni sem gilda 10% hvert, samtals 50% af lokaeinkunn.
- tvö hópverkefni þar sem hvort um sig gildir 20%, samtals 40% af lokaeinkunn.
- einstaklingsverkefni sem gildir 15–25% af lokaeinkunn.

---

> Útgáfa 0.3

| Útgáfa | Breyting                                                            |
| ------ | ------------------------------------------------------------------- |
| 0.1    | Fyrsta útgáfa                                                       |
| 0.2    | Bæta við kynningu í fyrirlestri; bæta við um Mux; uppfæra skiladags |
| 0.3    | Nánar um að setja inn routes fyrir yfirferð                         |

| 0.3    | Bæta við um Neon                                                    |
