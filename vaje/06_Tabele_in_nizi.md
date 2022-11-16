# Tabele in nizi

Namig: Pri reševanju nalog posušajte uporabiti raznolike metode razreda String, kot so `contains`, `format`, `split`, `toLowerCase`.

## Naloga 1

Napišite program, ki inicializira tabele, nato pa ročno nastavi vrednosti s pomočjo indeksov:

- `celaStevila` z velikostjo 3 in vrednostmi `1, 2, 3`
- `besede` z velikostjo 2 in vrednostma `hello, world`
- `crke` z velikostjo 4 in vrednostmi `a, b, c, d`

Na koncu izpiši število elementov posamezne tabele.

Izhod:

```text
celaStevila: 3
besede: 2
crke: 4
```

## Naloga 2

Napišite program, ki inicializira naslednje tabele:

- `celaStevila` z vrednostmi `10, 20, 30, 40, 50`
- `besede` z vrednostmi `vceraj, danes, jutri`
- `crke` z vrednostmi `x, y, z, w`

Na koncu naj za vsako izpiše število elementov posamezne tabele.

Izhod:

```text
celaStevila: 5
besede: 3
crke: 4
```

## Naloga 3

S pomočjo tabel sestavite program za izris kvadrata velikosti podane na vhodu, ki ne sme biti manjša od 3.

Vhod:

```text
4
```

Izhod:

```text
- - - -
- - - -
- - - -
- - - -
```

## Naloga 4

Predhodno nalogo nadgradite z možnostjo izrisa pravokotnika, kjer dolžina oz. širina stranice prav tako ne sme biti manjša od 3.

Vhod:

```text
pravokotnik
4x3
```

Izhod:

```text
- - - -
- - - -
- - - -
```

## Naloga 5

Napišite program, ki uporabnika najprej vpraša po podatkovnem tipu `char` ali `int`. Glede na njegov vhod zgenerirajte 5 naključnih znakov oziroma števil in mu omogočite, da desetkrat ugiba, če je vnešena vrednost v tabeli. Glede na vsebovanost vrednosti izpišite stanje (uspeh ali neuspeh) in na koncu izpišite koliko elementov je uspel ugotoviti ter kateri so bili vsi elementi v tabeli. V primeru, da uporabnik ugotovi vse vrednosti predčasno, prekinite možnost dodatnih poskusov.

Vhod:

```text
int
0
1
2
3
4
5
6
7
8
9
```

Izhod:

```text
Izbrano ugotavljanje števil.
0 ni v tabeli.
1 ni v tabeli.
2 ni v tabeli.
3 ni v tabeli.
4 je v tabeli.
5 je v tabeli.
6 ni v tabelo.
7 je v tabeli.
8 ni v tabeli.
9 ni v tabeli.
--------------
Ugotovljenih 3/5.
Preostale vrednosti:
15
21
```

## Naloga 6

Vojaki bi se na poziv _»V vrsto zbor!«_ morali razvrstiti po višini od najmanjšega do največjega, a tega ne znajo najbolje. Desetarja zanima, kdo je vsaj lokalno postavljen pravilno; ostale bo namreč kaznoval z dodatnimi sklecami. Vojak je postavljen lokalno pravilno, če je njegov levi sosed (če obstaja) nižji ali enako visok, desni sosed (če obstaja) pa višji ali enako visok kot on.

Napišite program, ki prebere zaporedje višin vojakov v »vrsti zbor« in izpiše indekse vseh
vojakov, ki so postavljeni lokalno pravilno. Če to ne velja za nikogar, naj program izpiše
NOBEDEN.

Vhod:

```text
10
185 172 180 181 190 183 178 185 191 207
```

Izhod:

```text
2
3
7
8
9
```

## Naloga 7

Športniki tekmujejo na teku na 60m z ovirami. Zaradi potreb naše naloge so spremenili pravila in imajo odslej na voljo dva poskusa, čas pa se meri le s celimi sekundami. Najmanjša vsota časa obeh poskusov da zmagovalca.

Sestavite program, ki bo na vhodu najprej sprejel število tekmovalcev ter shranil njihova imena. Nato naj se za posamezno ime izpiše možnost vnosa rezultatov obeh krogov. Na koncu naj se rezultati izpišejo v vrstnem redu od najhitrejšega (zmagovalca) navzdol z ustreznimi končnimi uvrstitvami.

Vhod:

```text
2
Alice Ableton
Bob Bradley
15
16
14
12
```

Izhod:

```text
Število tekmovalcev: 2
----------------------
Rezultati:
1.  Bob Bradley  (1p: 14s, 2p: 12s)  ...  26s
2.  Alice Ableton  (1p: 15s, 2p: 16s) ...  31s
```

## Naloga 8

Napišite poenostavljeno različico programa `sed`, ki podpira samo zamenjavo besedila. Kot prvi argument programa podprite dve stikali:

- `g`: globalna zamenjava niza (zamenjamo vse pojavitve prvotnega niza); privzeto naj se sicer zamenja samo prva pojavitev niza.
- `i`: upoštevamo iskanje po malih in velikih znakih (ang. _case insensitive_); privzeto naj se zamenja samo nize, ki so napisani v izvorni velikosti črk.

Uporabnik naj najprej vnese niz, ki ga želi zamenjati, nato niz za zamenjavo in na koncu še celotno besedilo.

Vhod:

```text
// Aplikacijo zaženemo kot:
// java naloga8 gi

svet
program
Pozdravljen, svet! Svet, pozdravljen.
```

Izhod:

```text
Pozdravljen, program! program, pozdravljen.
```

## Naloga 9

Sestavite program za štetje besed in izpis pogostosti pojavitve, ki služi kot osnova za algoritem TF.IDF (uporablja se v okviru strojnega učenja). Zajeti je potrebno vse besede, ki se pojavijo v besedilu in prešteti kolikokrat se pojavijo. Odstranite tudi vsa najpogostejša ločila (pika, vejica, dvopičje, podpičje, klicaj, pomišljaj, ...). Na koncu naj program izpiše seznam besed (naj bodo zapisane z malimi črkami) in število pojavitev v besedilu.

Vhod:

```text
Pozdravljen, svet! Program, pozdravljen.
```

Izhod:

```text
pozdravljen (2)
svet (1)
program (1)
```
