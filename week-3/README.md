# UrbanStyle – müügiandmete analüüs

## 1. Projekti ülevaade

Projekti eesmärk on analüüsida UrbanStyle'i müügi-, kliendi-, toote- ja turundusandmeid, kasutades SQL-päringuid ja andmebaasitabelite ühendamist. Analüüsi põhjal selgitame välja olulisemad müügitrendid, klientide ostukäitumise, toodete müügitulemused ning laoseisuga seotud probleemid.

## 2. Grupi esitlus

[UrbanStyle – grupi esitlus](https://docs.google.com/presentation/d/1V4vecJNvkw2XtjDkeAVUFLFo_mmHsj9XPD9e25hJWoQ/edit?slide=id.p1#slide=id.p1)

## 3. Grupi liikmed ja tööjaotus

| Grupi liige | Roll | Analüüsi teema |
|---|---|---|
| Maarja Valmas | Roll A | Müük ja kliendid |
| Marleen Aavere | Roll B | Kliendid ilma ostudeta |
| Marje Piirisild | Roll C | Tooted ja inventuur |
| Sigrid Nieländer | Roll D | Turunduskanalid ja müük |

### Individuaalsed töökaustad

- Maarja Valmas – [GitHubi link]
- Marleen Aavere – [GitHubi link]
- Marje Piirisild – [GitHubi link]
- Sigrid Nieländer – [GitHubi link]

## 4. Kasutatud andmetabelid

- `sales`
- `customers`
- `products`
- `inventory`

## 5. Kasutatud meetodid

Analüüsis kasutati SQL-päringuid ning järgmisi meetodeid:

- `INNER JOIN` ja `LEFT JOIN` tabelite ühendamiseks.
- `GROUP BY` andmete rühmitamiseks.
- `COUNT`, `SUM` ja `DISTINCT` andmete loendamiseks ja koondamiseks.
- `WHERE` tingimusi andmete filtreerimiseks.
- `ORDER BY` tulemuste järjestamiseks.

## 6. Peamised tulemused

### Roll A – Müükide ja klientide analüüs

**Eesmärk:** Ühendasin `sales`- ja `customers`-tabelid ning analüüsisin klientide ostusid, kogumüüki ja lojaalsustasemeid.

**Analüüsi tulemused:**

1. **TOP 10 klient:** suurima kogumüügiga klient oli Tiina Pärn (27 668,02 €).
2. **Enim oste linnade kaupa:** Tallinnas registreeriti 3601 ostu ning suurim kogumüük oli 1 006 252,88 €.
3. **Kogumüük lojaalsustaseme järgi:** kõige suurem kogumüük oli märkimata lojaalsustasemega klientidel (NULL) – 1 071 805,32 €.
4. **Teadaolevad lojaalsustasemed:** nende seas oli suurima kogumüügiga Silver-tase (593 470,07 €).
5. **Puuduv lojaalsustase:** 1260 kliendil ehk 40%-l kõigist 3150 kliendist puudus lojaalsustase.
6. **Üle keskmise kulutajad:** neid oli 763 ehk 29,90% ostnud klientidest (kokku 2552 ostnud klienti).

### Roll B – Kliendid ilma ostudeta

[Lisada analüüsi kokkuvõte.]

### Roll C – Toodete ja inventuuri analüüs

**Eesmärk:** Analüüsida toodete müügitulemusi ja laoseisu, tuvastada müümata tooted, selgitada välja edukaimad tooted ja tootekategooriad ning teha inventuuri täiendamise soovitusi.

**Analüüsi tulemused:**

1. **Müümata tooted:** LEFT JOIN-päringu abil tuvastasin 12 toodet, mille kohta müügikirjed puudusid. Kõige rohkem oli neid aksessuaaride kategoorias (5 toodet). Ülejäänud müümata tooted jagunesid naisterõivaste, lasterõivaste ja jalanõude kategooriate vahel (igaühes 2 toodet) ning meesterõivaste kategoorias (1 toode).

2. **TOP 10 suurima müügikäibega toodet:** suurima müügikäibega oli „Õhuline sünteetiline sporditossud“ (27 347,04 €, 35 müügikorda). Kõige rohkem müügikordi oli tootel „Õhuline linane jakk“ (41 müügikorda, 19 393,29 €). TOP 10 hulgas oli viis jalanõude, neli naisterõivaste ja üks meesterõivaste kategooria toodet.

3. **Müük kategooriate kaupa:** suurima kogumüügiga oli jalanõude kategooria (774 034,75 €), millele järgnesid meesterõivad (749 798,72 €) ja naisterõivad (686 464,24 €). Väikseima kogumüügiga oli lasterõivaste kategooria (305 844,45 €). Meesterõivaste kategoorias oli kõige rohkem tooteid (82) ja müügikirjeid (2266).

4. **Inventuuri analüüs:** ühendasin `products`- ja `inventory`-tabelid ning analüüsisin 1400 laoseisukirjet. Neist 1169 puhul oli laoseis piisav ja 231 puhul oli kogus võrdne tellimispunktiga või sellest väiksem. Negatiivse laoseisuga kirjeid oli 10. Kõikide toodete kohta oli inventuuris vähemalt üks vastav kirje.

**Ärilised järeldused ja soovitused:**

- Analüüsida 12 müümata toote müügipotentsiaali, hinda ja laoseisu ning kaaluda vajadusel allahindlust või sortimendist eemaldamist.
- Seada laoseisu täiendamisel prioriteediks suure müügikäibega tooted, eriti need, mille kogus on tellimispunktist väiksem.
- Pöörata erilist tähelepanu jalanõudele ja naisterõivastele, mis moodustasid suure osa TOP 10 toodetest.
- Kontrollida negatiivse laoseisuga kirjete õigsust ning jälgida varude olukorda regulaarselt eri asukohtades.

### Roll D – Turunduskanalid ja müük

[Lisada analüüsi kokkuvõte.]

## 7. Ärilised soovitused

[Lisada kogu meeskonna analüüsi põhjal tehtud soovitused UrbanStyle'i juhtkonnale.]