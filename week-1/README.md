# Week 1 – UrbanStyle Data Exploration

## 1. Eesmärk

Esimese nädala eesmärk oli tutvuda UrbanStyle'i andmebaasiga, uurida selle struktuuri, kontrollida andmete kvaliteeti ning saada ülevaade müügi-, kliendi- ja tooteandmetest.

## 2. Tehtud tööd

Meeskonnaliikmed analüüsisid nelja andmevaldkonda:

- **Sales:** müügitehingud.
- **Customers:** kliendiandmed.
- **Products:** tooteandmed.
- **Sales Channels & Locations:** müügikanalid ja asukohad.

Analüüsiks kasutasime SQL-päringuid andmete vaatamiseks, filtreerimiseks, loendamiseks ja andmekvaliteedi kontrollimiseks.

## 3. Andmete analüüs liikmete kaupa

### 3.1 Sales – müügitehingud

**Vastutaja:** Marje (Roll A)

**Tulemused:**
- Müügikirjeid kokku: **15 234**
- Korduvate müügi-ID-dega kirjeid: **5 116 (34%)**
- Puuduvad kliendi ID-d: **1 487 (10%)**
- Negatiivsed müügisummad: **305 (2%)**
- Suurim müügitehing: **2 170,40**
- Väikseim müügitehing: **–1 405,32**
- Puuduvad müügikirjed: **märts–november 2025**

**Peamine leid:** Müügiandmetes esineb korduvaid müügi-ID-sid, puuduvaid kliendi ID-sid ja negatiivseid müügisummasid. Need probleemid võivad mõjutada müügitulemuste usaldusväärsust.

**Soovitus:** Kontrollida duplikaate, selgitada välja negatiivsete summade põhjused ning kontrollida puuduva perioodi müügiandmeid.

### 3.2 Customers – kliendid

**Vastutaja:** Sigrid (Roll B)

**Tulemused:**
- Klientide arv: **3 150**
- Registreerimise periood: **02.01.2020–27.02.2025**
- Uusi kliente perioodil 01.07.2024–27.02.2025: **425**
- Erinevaid linnanimetusi: **54**
- Tallinna kliente täpse kirjapildi järgi: **1 135**
- Tallinna kliente kõiki kirjapilte arvestades: **1 184**
- Puuduvad e-posti aadressid: **380**
- Korduvaid e-posti aadresse: **130**

**Peamine leid:** Linnanimede kirjapilt on ebaühtlane ning kliendiandmetes esineb puuduvaid ja korduvaid e-posti aadresse. Tuvastati ka võimalikke duplikaatkliente, sealhulgas korduvate nimede ja sama kontaktinfoga kirjeid.

**Soovitus:** Ühtlustada linnanimede kirjapilt ning kontrollida võimalikke duplikaatkliente ka telefoninumbri või nime ja linna järgi.

**Töövihiku tähelepanek:** Korduvate e-posti aadresside arvutamisel tuleb kasutada valemit `COUNT(email) - COUNT(DISTINCT email)`, sest `COUNT(*)` arvestab sisse ka puuduvad e-posti aadressid.

### 3.3 Products – tooted

**Vastutaja:** Maarja (Roll C)

**Tulemused:**
- Toodete tabelis kokku: **362 rida**
- Unikaalseid tooteid: **350**
- Veerge: **9**
- Kategooriaid: **5**
- Meesteriided: **82**
- Jalanõud: **73**
- Naisteriided: **70**
- Lasteriided: **70**
- Aksessuaarid: **67**
- Jaehindade vahemik: **13,53–434,08 €**
- Korduvaid tootenimesid: **12**
- Puuduvad jaehinnad: **0**
- Puuduvad kategooriad: **0**
- Puuduvad ökosertifikaadi väärtused: **18**

**Peamine leid:** Toodete andmetes esines korduvaid tootenimesid ja puuduvaid ökosertifikaadi väärtusi. Lisaks leidus tooteid, mille jaehind oli omahinnast madalam.

**Soovitus:** Kontrollida korduvaid tootenimesid, täiendada puuduvat ökosertifikaadi infot ning vaadata üle tooted, mille jaehind on omahinnast madalam.

### 3.4 Sales Channels & Locations – müügikanalid ja asukohad

**Vastutaja:** Marleen (Roll D)

**Tulemused:**
- Müügikanaleid: **2** (online ja pood)
- Asukohti: **3** (Tallinn, Tartu ja Pärnu), lisaks NULL-väärtusega read.
- Makseviise: **3** (sularaha, kaart ja järelmaks)
- Tehinguid ilma asukohata: **5 204**

**Tehingud müügikanalite kaupa:**

| Müügikanal | Koos duplikaatidega | Ilma duplikaatideta |
|---|---:|---:|
| Pood | 10 030 | 6 656 |
| Online | 5 204 | 3 462 |

**Tehingud kaupluste kaupa:**

| Asukoht | Koos duplikaatidega | Ilma duplikaatideta |
|---|---:|---:|
| Tallinn | 5 704 | 3 801 |
| Tartu | 2 708 | 1 791 |
| Pärnu | 1 618 | 1 058 |

**Peamine leid:** Müügiandmetes on kaks müügikanalit ja kolm makseviisi. 5 204 tehingul puudub asukoha väärtus.

**Soovitus:** Kontrollida korduvaid tehinguid ning selgitada välja, kas asukohata kirjed on seotud veebimüügiga või puudulike andmetega.

## 4. Team Synthesis – ühine kokkuvõte

### Peamine järeldus

Olemasolevad andmed on puudulikud ja dubleeritud.

### Otsus

Andmed tuleb korrastada ja puhastada.

### Suurim üllatus

SQL on kiire ja mugav kasutada.

### Soovitus Toomasele

1. Tuvastada duplikaadid kõigis tabelites.
2. Selgitada välja negatiivsete tehingusummade põhjused.
3. Kontrollida väärtuseta (NULL) andmeid.
4. Ühtlustada linnanimede kirjapilt.

### Millised andmed puuduvad?

1. 2025–2026 müügitehingud.
2. Allahindluse protsent ja summa.
3. Käibemaks.
4. Käibemaksu andmed.
5. Tellimuse staatus.
6. Tagastuse tunnus.
7. Ökosertifikaatide info.
8. Asukohad.
9. E-posti aadressid.

## 5. Team Presentation

[Ühine Google Slides'i esitlus](https://docs.google.com/presentation/d/1OSvAZDeuVsxKY09hgog5AWu8bpQH22dgcPJkZZhqlKk/edit?slide=id.p)

## 6. Individual Portfolios

Iga meeskonnaliikme isiklikus portfoolios on tema enda SQL-päringud, analüüsi tulemused ja vajalikud ekraanipildid.

- **Roll A – Marje:** [GitHubi portfoolio](https://github.com/marjep1/daca-portfolio/tree/main/portfolio/week-1/team)
- **Roll B – Sigrid:** [GitHubi portfoolio](https://github.com/15sigrid/data-analyst-portfolio/tree/main/week-1)
- **Roll C – Maarja:** [GitHubi portfoolio](https://github.com/maarjavalmas/daca-portfoolio/tree/main/week-1)
- **Roll D – Marleen:** [GitHubi portfoolio](https://github.com/marleen-aavere/daca-portfolio)

## 7. Kasutatud tööriistad

- PostgreSQL
- Supabase
- SQL
- GitHub
- Google Slides

## 8. Meeskond

**SalesAnalytics – UrbanStyle'i müügiandmete analüüs.**
