# Week 2 – UrbanStyle Data Cleaning

## 1. Eesmärk

Teise nädala eesmärk oli puhastada UrbanStyle'i andmeid kolmes kriitilises domeenis (müük, kliendid, tooted) ning kontrollida tabelitevahelist kooskõla.

Toomas Kask (IT-juht, väljamõeldud juhtumi tegelane) seadis reegli: **testkoopia kõigepealt → puhasta → kontrolli → dokumenteeri**.

Kõik muudatused tehti **ainult testkoopiates** (`sales_test`, `customers_test`, `products_test`). Originaaltabelid jäid muutmata.

## 2. Kokkuvõte numbritena

| Domeen | Ridu enne | Leitud probleeme | Ridu pärast puhastamist | Vastutaja |
|---|---:|---:|---:|---|
| Sales | 15 234 | 6 653 | 10 118 | Marleen (Roll A) |
| Customers | 3 150 | 2 300 | 3 150 | Marje (Roll B) |
| Products | 362 | 38 | 350 | Sigrid (Roll C) |
| Ristvalideerimine | – | 604 | – | Maarja (Roll D) |

## 3. Tulemused rollide kaupa

### 3.1 Sales – müügiandmete puhastamine

**Vastutaja:** Marleen (Roll A)

| Kontroll | Leitud | Selgitus |
|---|---:|---|
| Duplikaatsed arved | 5 116 | Ligikaudu iga kolmas rida oli kordus; pärast eemaldamist 10 118 unikaalset rida |
| NULL väärtused | 1 487 | Puuduv customer_id; pärast duplikaatide eemaldamist 988. Külalisostud, mitte viga – read säilitati |
| Võimatud kuupäevad | 50 | Müügid pärast andmete lõppkuupäeva 2025-02-28 (tuleviku kuupäevi 0). Märgistati, ei kustutatud |
| Hilised kuupäevad pärast duplikaatide eemaldamist | 32 | Jäetakse analüüsist välja; analüüsiks sobib 10 086 rida |
| Lisaleid: müügisumma ≠ jaehind × kogus | 664 | Erinevus > 1 €. Ei tähenda viga, hinnad vajavad täiendavat kontrolli (edasijõudnute tase) |

**Peamine leid:** Duplikaadid moonutasid varasemates aruannetes müügitulu ja tehingute arvu – ligikaudu iga kolmas rida oli kordus.

**Soovitus:** Kasutada müügianalüüsis puhastatud 10 086 rida ja otsustada, kuidas käsitleda andmete lõppkuupäevast hilisemaid kirjeid.

### 3.2 Customers – kliendiandmete puhastamine

**Vastutaja:** Marje (Roll B)

| Kontroll | Leitud | Selgitus |
|---|---:|---|
| Duplikaatsed e-mailid | 258 | 128 e-posti aadressi esineb mitmel real; neist 146 rida ilma müügitehinguteta |
| NULL eesnimi / perenimi | 0 | Nimed olemas |
| Ühtlustamata ees- / perenimed | 150 | Eesnimed 125, perenimed 25 |
| Ebajärjekindlad linnanimed | 252 | 54 kirjaviisi → 12 linna |
| NULL telefon / e-mail | 380 | Puuduv e-posti aadress |
| NULL loyalty tier | 1 260 | Lojaalsustase teadmata |

**Peamine leid:** Linnanimedes oli 54 kirjaviisi 12 linna kohta; pärast standardiseerimist on linnad ühtsed.

**Soovitus:** Käsitleda duplikaatsed e-postid ja puuduvad väärtused enne, kui klientide andmeid analüüsis kasutatakse.

### 3.3 Products – tooteandmete puhastamine

**Vastutaja:** Sigrid (Roll C)

| Kontroll | Leitud | Selgitus |
|---|---:|---|
| Duplikaatsed tootenimed | 12 | Sama nimi 2 korda, duplikaadid ID-dega 1351–1362 on kustutatud products_test-ist, tabelis nüüd 350 rida |
| NULL nimi / kategooria / hinnad | 0 | Kriitilised väljad on täidetud |
| Negatiivne või äärmuslik jaehind | 0 | Kalleim toode 434,08 € |
| Ebajärjekindlad kategooriad | 0 | 5 kategooriat, igaüks ühes kirjapildis |
| Lisaleid: jaehind < omahind | 8 toodet | 10 rida, millest 2 on duplikaadid |
| Lisaleid: `eco_certified` = NULL | 18 | NULL ≠ false: sertifikaadi olemasolu teadmata |

**Peamine leid:** 8 toote jaehind on omahinnast madalam. Vajab äripoole kontrolli, kas tegu on andmevea või tegeliku kahjumiga müügiga.

**Soovitus:** Viia duplikaatide eemaldamine originaaltabelisse ja kontrollida kahjumiga hindadega tooteid enne marginaalianalüüsi.

**Duplikaatide kustutamine:** Duplikaadid on products_test-ist kustutatud ja kontrollitud: alles 350 rida, korduvaid tootenimesid 0. Enne kustutamist kontrolliti, et ükski müük ei viita duplikaatidele.

### 3.4 Ristvalideerimine ja kvaliteedikontroll

**Vastutaja:** Maarja (Roll D)

| Kontroll | Leitud | Selgitus |
|---|---:|---|
| Müügid olematule kliendile | 0 | Kõik müügitabeli kliendiviited vastasid olemasolevatele klientidele. |
| Müügid olematule tootele | 0 | Kõik müügitabeli tooteviited vastasid olemasolevatele toodetele. |
| Kliendid, kes pole ostnud | 592 | 592 kliendil puudusid ostutehingud. |
| Tooted, mida pole müüdud | 12 | 12 toodet ei olnud müügitabelis kordagi esindatud. |

**Peamine leid:** Müügitabeli kliendi- ja tooteviited olid korras, kuid 592 klienti polnud kunagi ostnud ning 12 toodet polnud kordagi müüdud. Need tulemused vajavad ärilist ülevaatamist kuid ei tähenda automaatselt vigaseid andmeid.

**Soovitus:** Soovitan üle vaadata ostuta kliendid ja müümata tooted ning hinnata, kas nende kirjete puhul on vaja midagi muuta või on tegemist tavapärase äritegevusega.

## 4. Team Synthesis – ühine kokkuvõte

### Suurim üllatus
12 toodet, mida pole kordagi müüdud (Roll D), on samad 12 duplikaattoodet (ID-d 1351–1362), mille leidis Roll C. Duplikaadid said uued ID-d, seepärast neile müüke ei viita – kaks eri kontrolli kinnitasid sama leidu.

### Soovitus Toomasele
1. [ ]
2. [ ]
3. [ ]

### Milliseid andmeid meil puudus?
1. [ ]
2. [ ]

### Osakondade sild

**Meie osakond:** Müük

**Number enne → pärast puhastamist:** tooteid 362 → 350 (12 duplikaati kustutatud products_test-ist, kontrollitud)

**Päring:** `SELECT COUNT(*) AS enne, COUNT(DISTINCT product_name) AS parast FROM products;`

**Mida see osakonnale tähendab:** tootekataloogis oli 12 duplikaatset toodet, tegelik toodete arv on 350, mitte 362.

**Teiselt meeskonnalt:**  Klienditeenindus – e-posti aadresside kontroll. Enne 2770, pärast 2640. Kontrollisin päringut oma `customers_test` tabelis ja sain täpselt samad tulemused. Tulemus: sama.

### Kaizen (nano-parendus järgmiseks nädalaks)
Järgmisel nädalal võiks enne andmete analüüsimist teha kiire kontroll, et duplikaadid ja puuduvad väärtused saaksid kohe märgatud.

## 5. Team Presentation

- Meeskonna esitlus (Google Slides) https://docs.google.com/presentation/d/1qQ7wK_4pNYztKWZQMCtan6fLj89MBDSxOG7baWZOtis/edit?usp=sharing

## 6. Individual Portfolios

Iga liikme isiklikus portfoolios on tema puhastamisskript (`week2_[domeen]_cleaning.sql`) ja README.

- **Roll A – Marleen:** [GitHubi link](https://github.com/marleen-aavere/daca-portfolio/blob/main/week-2/team_sales_analytics.md)
- **Roll B – Marje:** [GitHubi link](https://github.com/marjep1/daca-portfolio/tree/main/portfolio/week-2/team)
- **Roll C – Sigrid:** [GitHubi portfoolio](https://github.com/15sigrid/data-analyst-portfolio/tree/main/week-2)
- **Roll D – Maarja:** [GitHubi link](https://github.com/maarjavalmas/daca-portfoolio/tree/main/week-2)

## 7. Kasutatud tööriistad

- PostgreSQL / Supabase
- SQL: `GROUP BY` + `HAVING`, `ROW_NUMBER()`, `COALESCE`, `CASE WHEN`, `INITCAP`, `TRIM`, `UPDATE`, `DELETE`
- GitHub

## 8. Meeskond

**SalesAnalytics – UrbanStyle'i müügiandmete analüüs.**
