# Zanke

## Naloga 1

Napišite program, ki na izhod izpiše prvih 10 naravnih števil. Najprej naj bodo vsa izpisana v prvi vrstici, nato pa posamezno število z izjemo prvega v svoji vrstici tako, da bodo prikazana diagonalno.

Izhod:

```text
1 2 3 4 5 6 7 8 9 10
  2
    3
      4
        5
          6
            7
              8
                9
                  10
```

V kolikor želite, lahko program dopolnite tako, da bodo števila izpisana po obeh diagonalah in še vsa v zadnji vrstici.

```text
1 2 3 4 5 6 7 8 9 10
  2             9
    3         8
      4     7
        5 6
        6 6
      4     7
    3         8
  2             9
1 2 3 4 5 6 7 8 9 10
```

## Naloga 2

Napišite program, ki na vhodu sprejme poljubno celo število v rangu od 10 do 1000. V kolikor je vhodni podatek napačen, izpišite opozorilo o napaki. Napišite logiko, ki sešteje vsa števila od 1 do vključno podanega števila na vhodu.

Vhod:

```text
15
```

Izhod:

```text
Rezultat: 120
```

## Naloga 3

Napišite program, ki omogoči uporabniku vnos desetih poljubnih števil. Števila med seboj zmnožite, na koncu pa poleg rezultata zmnožka izpišite še njihovo povprečje.

Vhod:

```text
1
2
3
4
5
6
7
8
9
10
```

Izhod:

```text
Zmnožek: 3628800
Povprečje: 5,5
```

## Naloga 4

Napišite program, ki omogoči izris pravokotnega trikotnika s pomočjo zvezdic. Na vhodu od uporabnika sprejmite poljubno celo število, večje od 3, ki določa velikost trikotnika. V primeru napačnega vhodnega podatka, to uporabniku sporočite.

Vhod:

```text
5
```

Izhod:

```text
*
**
***
****
*****
```

## Naloga 5

Napišite program, ki od uporabnika zahteva vnos besedila toliko časa, dokler ne zapiše besede `konec`. Pri tem naj program shrani število ponovitev vnosa in na koncu ta podatek uporabniku izpiše.

Vhod:

```text
asd
bfg
cghj
djur
euuz
fruijh
kgii
konec
```

Izhod:

```text
Število ponovitev vnosa: 7
```

## Naloga 6

Napišite program, ki na vhodu sprejme dve celi števili, ki predstavljata leto, pri čemer mora biti prvo manjše od drugega. V primeru napačnega vrstnega reda izpišite napako. Za vsa vmesna leta preverite ali je katero izmed njih prestopno in to ustrezno izpišite nad izhod.

Vhod:

```text
2015
2025
```

Izhod:

```text
Leto 2016 ni prestopno leto.
Leto 2017 ni prestopno leto.
Leto 2018 ni prestopno leto.
Leto 2019 ni prestopno leto.
Leto 2020 je prestopno leto. <-
Leto 2021 ni prestopno leto.
Leto 2022 ni prestopno leto.
Leto 2023 ni prestopno leto.
Leto 2024 je prestopno leto. <-
```

## Naloga 7

Ustvarite program, ki prebere celi števili označeni z `a` in `b` in izpiše njihove kvadrate v zaporedju od `a` do `b`.

Vhod:

```text
5
8
```

Izhod:

```text
a=5
b=8
---
5^2 = 25
6^2 = 36
7^2 = 49
8^2 = 64
```

## Naloga 8

Napišite program, ki prebere celo število in izpiše število njegovih števk. Namig: Da celemu številu odstranimo najbolj desno števko, ga lahko delimo z 10.

Vhod:

```text
869436
```

Izhod:

```text
Vhodno število: 869436
Število števk: 6
```

## Naloga 9

Program iz prejšnje naloge nadgradite tako, da pred končnim izpisom izpiše še vse števke v obratnem vrstnem redu.

Izhod:

```text
6
3
4
9
6
8
---
Vhodno število: 869436
Število števk: 6
```

## Naloga 10

Collatzovo zaporedje pričnemo s podanim celim številom `n`, nato pa ponavljamo sledeči postopek, dokler ne pridemo do števila 1:

- če je trenutno število sodo, ga delimo z 2
- v nasprotnem primeru število pomnožimo s 3 in mu prištejemo 1

Opisani postopek bi nas za vsako pozitivno celo število moral pripeljati do enice. Glede na podano vhodno število izpište število členov zaporedja.

Primer za število 7, kjer dobimo zaporedje s 17 členi (štejemo tudi začetno 7):
7 -> 22 -> 11 -> 34 -> 17 -> 52 -> 26 -> 13 -> 40 -> 20 -> 10 -> 5 -> 16 -> 8 -> 4 -> 2 -> 1

Vhod:

```text
7
```

Izhod:

```text
Vhodno število: 7
Število členov v Collatzovem zaporedju: 17
```

## Naloga 11

Prejšnjo nalogo nadgradite tako, da na vhodu sprejmete dve celi števili, ki tvorita rang. V okviru tega ranga preverite število členov zaporedja za vsako število. Število z najdaljšim zaporedjem in pripadajočim številom členov izpišite na izhod.

Vhod:

```text
10
20
```

Izhod:

```text
Število z najdaljšim zaporedjem med 10 in 20 je: 18
Število členov zaporedja števila 18: 21
```

## Naloga 12

Napišite program, ki na vhodu prebere pozitivno celo število `a`, nato pa nariše piramido zvezdic višine `a`.

Vhod:

```text
4
```

Izhod:

```text
   *
  ***
 *****
*******
```

## Naloga 13

Kolesar je pozabil točno kombinacijo števične ključavnice, ki jo je uporabil za zavarovanje kolesa pri shranjevanju v kolesarnico. Ključavnica ima tri številska mesta (a-b-c). Kolesar se spomni, da je prva števka liha, druga večja od `m`, tretja pa deljiva z `d`. Napišite program, ki prebere števili `m` in `d` ter izpiše vse možne kombinacije števk ter njihovo skupno število.

Vhod:

```text
7
3
```

Izhod:

```text
1-8-0
1-8-3
1-8-6
1-8-9
1-9-0
1-9-3
1-9-6
1-9-9
3-8-0
3-8-3
3-8-6
3-8-9
3-9-0
3-9-3
3-9-6
3-9-9
5-8-0
5-8-3
5-8-6
5-8-9
5-9-0
5-9-3
5-9-6
5-9-9
7-8-0
7-8-3
7-8-6
7-8-9
7-9-0
7-9-3
7-9-6
7-9-9
9-8-0
9-8-3
9-8-6
9-8-9
9-9-0
9-9-3
9-9-6
9-9-9
40
```

## Naloga 14

Množična odprtja trgovin so pripeljala do večjega števila nepotrebnih nakupov. Ena od metod preprečevanja zapravljanja je uvedba pametnih košaric, ki sprejmejo največ deset artiklov. Zatem se zaklenejo in kupec lahko takšno košarico le še odnese na blagajno. Obstaja dodatno pravilo, ki sproži zaklep v kolikor cena doseže ali preseže ceno 100 enot.

Napišite program v katerem uporabnik na vhodu vnaša cene artiklov, ki jih sproti dodaja v košarico. Program naj preneha z nadaljnjim izvajanjem ko je izpolnjen en izmed pogojev:

- vnos števila 0 (pomeni, da je z dodajanjem artiklov prenehal)
- vnešenih deset števil (oziroma cen artiklov)
- vsota cen doseže ali preseže 100 enot

V primeru, da kupec vnese število 0, se to ne smatra kot dodan artikel. Po zaključku vnosa podatkov, naj program izpiše število dodanih artiklov v košarico in njihovo skupno ceno.

Vhod:

```text
Cena: 10
Cena: 5
Cena: 0
```

Izhod:

```text
V košarico ste dodali 2 artikla, ki skupaj znašata 15 enot.
```

## Naloga 15

Napišite program, ki na vhodu sprejme celo število in izpiše vse njegove delitelje.

Vhod:

```text
18
```

Izhod:

```text
1
2
3
6
9
18
```
