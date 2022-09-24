# Podatkovni tipi

Java je močno tipiziran jezik, kar pomeni, da moramo spremenljivkam določiti njihov podatkovni tip. Obstaja osem _primitivnih_ tipov:

- 4 celoštevilski _(ang. integer)_
- 2 številska s plavajočo vejico _(ang. floating-point number)_
- 1 logični _(ang. boolean)_
- 1 znakovni _(ang. character)_

## Cela števila

Celoštevilski podatkovni tipi so namenjeni zapisu števil brez decimalnega dela. Dovoljena so tako pozitivna, kot tudi negativna števila.

| Tip   | Velikost [bajt] | Min. vrednost        | Max. vrednost       |
| ----- | --------------- | -------------------- | ------------------- |
| byte  | 1               | -128                 | 127                 |
| short | 2               | -32768               | 32767               |
| int   | 4               | -2147483648          | 2147483647          |
| long  | 8               | -9223372036854775808 | 9223372036854775807 |

V večini primerov je najbolj praktičen tip `int`. Za predstavitev največjih števil uporabimo `long`. `byte` in `short` sta tipa, namenjena zelo specifični uporabi - na primer pri nizkonivojskem delu z datotekami ali ko je število podatkov takšno, da s tem uspemo bistveno prihraniti na prostoru za njihovo shranjevanje (če nam to seveda dovoljuje velikost vrednosti števil).

Dejanski razpon števil glede na posamezen tip je v Javi fiksen, kar pomeni, da arhitekturna vrsta procesorja nanje ne vpliva. Tako smo pri uporabi naših programov na različnih platformah varni, saj nam ni potrebno skrbeti kaj se zgodi, če zaženemo program na sistemih s 16-bitnim ali 32-bitnim procesorjem. Pri nekaterih drugih programskih jezikih je velikost podatkovnega tipa namreč pogojena z vrsto arhitekture.

Pri zapisu števil si lahko pomagamo s predponami in priponami:

- za števila tipa `long` uporabimo pripono `L` ali `l`, na primer: `4000000000L`
- za šestnajstiška števila uporabimo predpono `0x` ali `0X`, na primer: `0xABCD`
- za omiška števila uporabimo predpono `0`, na primer: `010`
- za dvojiška števila uporabimo predpono `0b` ali `0B`, na primer: `0b1001`

Za lažje branje števil smemo pri zapisu uporabiti podčrtaj, na primer: `1_000_000`, `0b1111_0100_0010_0100_0000`. Podčrtaji so vidni le v kodi, pred prevajanjem pa jih prevajalnik enostavno izbriše.

## Števila s plavajočo vejico

Števila s plavajočo vejico so namenjena zapisu decimalnih števil.

| Tip    | Velikost [bajt] | Natančnost         | Min. vrednost [10^]  | Max. vrednost [10^] |
| ------ | --------------- | ------------------ | -------------------- | ------------------- |
| float  | 4               | 7 decimalnih mest  | -128                 | 127                 |
| double | 8               | 15 decimalnih mest | -32768               | 32767               |

Poimenovanje tipa `double` izhaja iz razloga dvakratne natančnosti v primerjavi s tipom `float` (`double` - 8 B, `float` - 4 B). Omejena natančnost tipa `float` v mnogo primerih ne zadostuje, zato je potrebno pred njegovo uporabo dobro premisliti. V kolikor prostorsko za shranjevanje decimalnih števil nimamo posebnih omejitev, je smiselneje izbrati kar tip `double`.

Pri zapisu decimalnih števil si lahko pomagamo s priponami:

- za `float` uporabimo pripono `F` ali `f`, na primer: `3.14F`
- za `double` se štejejo vsa števila zapisana v decimalni obliki, opcijsko pa lahko uporabimo pripono `D` ali `d`, na primer: `3.14D`

Vsi izračuni nad števili s plavajočo vecijo sledijo specifikaciji IEEE 754. Obstajajo tri posebne vrednosti tovrstnih števil, namenjene označevanju poseganja prek meja _(ang. overflow)_ in napak:

- pozitivna neskončnost _(primer: deljenje pozitivnega števila z 0)_
- negativna neskončnost
- NaN _(ang. not a number)_ - ni število _(primer: deljenje števila 0 z 0)_

Opozoriti moramo samo še, da števila s plavajočo vejico niso primerna za izračune iz finančnega področja. Težava je namreč v tem, da pri zaokroževanju po izračunih pogosto pride do napak zaradi načina obravnave teh števil.

## Logične vrednosti

Tip `boolean` je namenjen zapisu logičnih vrednosti `true` in `false`. Uporabljen je pri preverjanju logičnih pogojev.

## Znaki

Tip `char` je bil izvorno namenjen zapisu posameznih znakov, vendar se je z razvojem programskega jezika to spremenilo. V ozadju se za zapis znakov uporablja Unicode, ki za določene znake zahteva eno `char` vrednost, spet pri drugih pa dve. Podrobnosti zapisa znakov si bomo pogledali v enem izmed kasnejših poglavij.

Bistveno za zapis znakov je zaenkrat le, da uporabimo enojne navednice poleg znaka, ki ga želimo zapisati, na primer: `'a'`.

## Nizi

Poleg zapisa posameznih znakov, pogosto v programih želimo delati tudi z besedili. V ta namen uporabimo nize, ki pa niso del primitivnih podatkovnih tipov, temveč sestavljenih. Tip niza je `String`, za zapis njegove vrednosti pa uporabimo dvojne navednice, na primer: `"Pozdravljen, svet!"`.
