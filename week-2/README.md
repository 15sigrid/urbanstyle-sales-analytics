# Week 2 – UrbanStyle Data Cleaning

## 1. Eesmärk

Teise nädala eesmärk oli puhastada UrbanStyle'i andmeid kolmes kriitilises domeenis (müük, kliendid, tooted) ning kontrollida tabelitevahelist kooskõla.

Toomas Kask (IT-juht, väljamõeldud juhtumi tegelane) seadis reegli: **testkoopia kõigepealt → puhasta → kontrolli → dokumenteeri**.

Kõik muudatused tehti **ainult testkoopiates** (`sales_test`, `customers_test`, `products_test`). Originaaltabelid jäid muutmata.

## 2. Kokkuvõte numbritena

| Domeen | Ridu enne | Leitud probleeme | Ridu pärast puhastamist | Vastutaja |
|---|---:|---:|---:|---|
| Sales | 15 234 | 6 653 | 10 118 | Marleen (Roll A) |
| Customers | 3 150 | [ ] | [ ] | Marje (Roll B) |
| Products | 362 | 38 | 350 | Sigrid (Roll C) |
| Ristvalideerimine | – | [ ] | – | Maarja (Roll D) |

## 3. Tulemused rollide kaupa

### 3.1 Sales – müügiandmete puhastamine

**Vastutaja:** Marleen (Roll A)

| Kontroll | Leitud | Selgitus |
|---|---:|---|
| Duplikaatsed arved | [ ] | |
| NULL väärtused | [ ] | |
| Võimatud kuupäevad | [ ] | |
| [ ] | [ ] | |

**Peamine leid:** [1–2 lauset]

**Soovitus:** [1 lause]

### 3.2 Customers – kliendiandmete puhastamine

**Vastutaja:** Marje (Roll B)

| Kontroll | Leitud | Selgitus |
|---|---:|---|
| Duplikaatsed e-mailid | [ ] | |
| NULL eesnimi / perenimi | [ ] | |
| Ebajärjekindlad linnanimed | [ ] | |
| NULL telefon / e-mail | [ ] | |

**Peamine leid:** [1–2 lauset]

**Soovitus:** [1 lause]

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
| Müügid olematule kliendile | [ ] | |
| Müügid olematule tootele | [ ] | |
| [ ] | [ ] | |

**Peamine leid:** [1–2 lauset]

**Soovitus:** [1 lause]

## 4. Team Synthesis – ühine kokkuvõte

### Suurim üllatus
[1–2 lauset andmete kohta]

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

**Teiselt meeskonnalt:** [Maarja täidab pärast teise meeskonna päringu kontrolli]

### Kaizen (nano-parendus järgmiseks nädalaks)
[1 lause]

## 5. Team Presentation

[Link esitlusele]

## 6. Individual Portfolios

Iga liikme isiklikus portfoolios on tema puhastamisskript (`week2_[domeen]_cleaning.sql`) ja README.

- **Roll A – [nimi]:** [GitHubi link]
- **Roll B – [nimi]:** [GitHubi link]
- **Roll C – Sigrid:** [GitHubi portfoolio](https://github.com/15sigrid/data-analyst-portfolio/tree/main/week-2)
- **Roll D – [nimi]:** [GitHubi link]

## 7. Kasutatud tööriistad

- PostgreSQL / Supabase
- SQL: `GROUP BY` + `HAVING`, `ROW_NUMBER()`, `COALESCE`, `CASE WHEN`, `INITCAP`, `TRIM`, `UPDATE`, `DELETE`
- GitHub

## 8. Meeskond

**SalesAnalytics – UrbanStyle'i müügiandmete analüüs.**
