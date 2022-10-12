# Pogojni stavki

## Naloga 1

Napišite program, ki uporabniku ponudi možnost vnosa števila. Na osnovi vnesene vrednosti preverite ali je vnesel enomestno ali večmestno število in to tudi izpišite.

Vhod:

```text
5
```

Izhod:

```text
Vhod: 5
Število je enomestno.
```

## Naloga 2

Dopolnite prejšnjo nalogo tako, da poleg enomestnega števila preverjate še:

- dvomestno
- tromestno
- štirimestno
- petmestno
- šestmestno

V primeru, da ima število več mest izpišite, da gre za večmestno število.

Vhod:

```text
1234
```

Izhod:

```text
Vhod: 1234
Število je štirimestno.
```

## Naloga 3

Sestavite program, ki na vhodu prebere dve decimalni števili označeni kot `a` in `b`. Po sprejemu podatkov ugotovite katero število je večje in katero manjše. Na koncu vhodna podatka in ugotovitev izpišite. V primeru enakosti izpišite, da sta števili enaki.

Vhod:

```text
14.72
23.58
```

Izhod:

```text
a=14.72 <- Manjše
b=23.58 <- Večje
-------
Števili se razlikujeta.
```

## Naloga 4

Napišite program, ki na vhodu sprejme celo število. Zanimata nas dve lasnosti tega števila in sicer:

- sodost/lihost
- pozitivnost/negativnost

Po preverjanju obeh lastnosti uporabniku z izpisom na izhod sporočite rezultat.

Vhod:

```text
8
```

Izhod:

```text
Število 8 je sodo in pozitivno.
```

## Naloga 5

Ustvarite program, ki na vhodu sprejme 3 cela števila označena z `a`, `b` in `c` ter jih primerja po velikosti. Na izhod najprej izpiše vhodne podatke, nato vrstni red velikosti od največjega do najmanjšega in na koncu še katero število po vrsti vnosa je bilo največje.

Vhod:

```text
23
8
45
```

Izhod:

```text
a=23
b=8
c=45

Razvrstitev po velikosti:
1. 45 (c)
2. 23 (a)
3. 8 (b)

Največje izmed vnešenih števil je bilo c=45.
```

## Naloga 6

Napišite program, ki na vhodu sprejme cifro. Po vnosu podatka preverite ali je dejanska cifra in v primeru napake izpišite, da je vhodni podatek napačen. V primeru pravilnosti podatka izpišite ime cifre z besedo.

Vhod:

```text
7
```

Izhod:

```text
sedem
```

## Naloga 7

Operater, ki ponuja klicne storitve ima naslednji cenik:

| Trajanje klica (v sekundah) | Cena (enot na sekundo) |
| --------------------------- | ---------------------- |
| 1-500                       | 0,01                   |
| 501-800                     | 0,008                  |
| 801+                        | 0,005                  |

Obstajajo trije osnovni paketi, ki vključujejo samo prenos podatkov - uporabnik mora biti na paket obvezno naročen:

| Paket | Prenos | Cena (enot) |
| ----- | ------ | ----------- |
| Mini  | 1 GB   | 10          |
| Midi  | 2 GB   | 20          |
| Maxi  | 3 GB   | 30          |

Uporabnika na vhodu povprašajte po imenu njegovega paketa in sekundah klicev, ki jih je opravil v mesecu. Preverite, da so vnešeni podatki pravilni - veljaven paket in ustrezno pozitivno število sekund. V primeru napačnega vnosa uporabnika opozorite na napako. V kolikor uporabnik pravilno vnese podatke, mu izpišite končni izračun cene.

Pozor: V kolikor uporabnik opravi 550 sekund klicev, se prvih 500 obračuna po ceni 0,01, preostalih 50 pa po 0,008.

Vhod:

```text
Mini
495
```

Izhod:

```text
Vaš paket: Mini (10 enot)
Opravljenih sekund klicev: 495 (495 * 0,01 + 0 * 0,008 + 0 * 0,005 = 4,95)
------------------
Končna cena: 10 + 4,95 = 14,95 enot
```

## Naloga 8

Ob koncu šolskega leta boste pridobili skupno oceno posameznega predmeta. Osredotočimo se na predmete:

- računalništvo
- laboratorijske vaje iz računalništva
- matematika

Uporabnika povprašajte po skupni oceni za vsak predmet in mu omogočite vnos podatka. Na koncu izračunajte povprečje teh ocen in vrednost shranite v poljubno spremenljivko. Izpišite ocene po posameznih predmetih in povprečje.

Izhod:

```text
Skupna ocena za računalništvo: 5
Skupna ocena za laboratorijske vaje iz računalništva: 5
Skupna ocena za matematiko: 5

Povprečje ocen: 5.0
```

## Naloga 9

Nadgradite program iz prejšnje naloge tako, da na osnovi povprečja ocen uporabniku izpišete sporočilo:

- enako 5: Odlično!
- enako 4: Prav dobro!
- manjše od 4: Dobro?
- enako 1: Izboljšaj ocene!

Izhod:

```text
Skupna ocena za računalništvo: 5
Skupna ocena za laboratorijske vaje iz računalništva: 5
Skupna ocena za matematiko: 5

Povprečje ocen: 5. Odlično!
```

## Naloga 10

Predpostavimo, da ste opravili nakup enega Bitcoina. Glede na situacijo je nihanje cene precejšnje, zato nas zanima kakšno je trenutno stanje vaše investicije. Napišite program, ki na vhodu najprej sprejme ceno v FIAT valuti po kateri ste kupili Bitcoin, zatem pa še trenutno ceno v isti valuti. Na osnovi obeh podatkov opravite izračun dobička ali izgube in uporabniku sporočite oba vhodna podatka, razliko in odstotek spremembe.

Izhod:

```text
Nakupna cena: 55000
Trenutna cena: 20000
Razlika: -35000
Sprememba: -63,64%
```

## Naloga 11

Dopolnite prejšnjo nalogo tako, da uporabniku na osnovi spremembe (v odstotkih) izpišete sporočilo:

- več od 100%: Čestitamo, vaše špekulacijske sposobnosti so neprecenljive!
- od 5% do 100%: Odličen nakup, uspešno ste povečali svoje premoženje!
- od -5% do 5%: Investicija čaka na boljše čase.
- od -50% do -5%: Trend kot kaže ni obetaven.
- od -75% do -50%: Čas za dodatne nakupe?
- manj od -75%: Več sreče prihodnjič. HODL.

Izhod:

```text
Nakupna cena: 55000
Trenutna cena: 20000
Razlika: -35000
Sprememba: -63,64%

Stanje: Čas za dodatne nakupe?
```
