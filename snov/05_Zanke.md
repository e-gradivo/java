# Zanke

V tem poglavju se spoznamo z dodatnimi krmilnimi stavki, ki jih uvrščamo med zanke. Bistveno zanje je, da na osnovi podane logične predpostavke izvršujejo zaporedje stavkov v bloku toliko časa, dokler je ta predpostavka veljavna. Pri preverjanju veljavnosti predpostavke se zanašamo na operatorje, ki smo jih spoznali pri pogojnih stavkih.

Vse zanke so sestavljene iz pogojnega stavka in bloka, ki vključuje zaporedje stavkov, izvajajočih se dokler je pogojni stavek veljaven. Spoznali bomo tri različne zanke `while`, `do-while` in `for`, ki jih uporabljamo glede na ustreznost v dani situaciji.

## `while`

Zanka `while` sestoji iz oblike `dokler (pogoj) stavek` oziroma `while (condition) statement`. Poenostavljeno napisano, dokler je pogojni stavek veljaven, se stavek izvaja.

```java
int stevec = 0;

while (stevec < 10) {
    System.out.println(stevec);
    stevec++;
}
```

Potek izvajanja zanke `while` je podoben pogojnemu stavku `if`, ki pred izvajanjem bloka najprej preveri veljavnost pogoja. V primeru, da je pogoj pravilen, se blok s stavki prične izvajati. Po zaključku bloka, se izvajanje ne nadaljuje za blokom, kot je to pri pogojnem stavku, temveč se vrne na začetek, k ponovnemu preverjanju veljavnosti pogoja. V primeru, da je pogoj še vedno veljaven, se pričnejo izvajati stavki v bloku, sicer pa se izvajanje nadaljuje z naslednjim ukazom takoj za blokom zanke.

V zgornjem primeru smo se v pogoju zanašali na vrednost spremenljivke `stevec`, ki smo jo definirali na začetku programa. Če preverimo celoten potek zanke ugotovimo, da se bo ta izvajala vse dokler vrednost spremenljivke ne postane `10`. Povečevanje vrednosti spremenljivke se dogaja v bloku, ki jo postopoma z vsakim izvajanjem spremeni. Pred stavkom, kjer se povečevanje zgodi, se vrednost spremenljivke še izpiše. Tako po zaključku izvajanja programa pridobimo naslednji rezultat:

```text
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

V zankah pogosto uporabljamo splošno spremenljivko, katere vrednost se tekom izvajanja zanke spreminja in hkrati določa tudi prihodnje stanje, na katerem zanka temelji.

## `do-while`

Zanka `do-while` je zapisana v obliki `opravi stavek dokler (pogoj)` oziroma `do statement while (condition)`. Spreminja logiko preverjanja pogoja, saj se pred tem že izvede stavek.

```java
int stevec = 5;

do {
    System.out.println(stevec);
    stevec--;
} while (stevec < 5 && stevec >= 0); // prvi del pogoja sicer ne spremeni te zanke, lahko pa primerjamo način delovanja z while zanko
```

Potek izvajanja zanke `do-while` je obraten zanki `while`. Najprej se izvede blok zanke ne glede na pogoj, šele po zaključku izvajanja bloka pa se preveri veljavnost pogoja. Na njegovi osnovi se izvede ponovno izvajanje oziroma izstop iz zanke in nadaljevanje z naslednjimi ukazi programa.

V zgornjem primeru smo na začetku programa definirali spremenljivko `stevec`, ki zopet določa kolikokrat se zanka izvede. Zatem se ne glede na pogoj prične izvajati blok zanke, ki izpiše trenutno vrednost spremenljivke in jo zmanjša za 1. Sledi preverjanje pogoja v katerem velja, da mora biti `stevec` manjši od `5` in pozitiven ali enak `0`. Do pogoja se v postopku vrednost spremenljivke že zmanjša na `4`, zato je ta veljaven in omogoči vnovično izvajanje bloka zanke. Po zaključku izvajanja pridobimo naslednji rezultat:

```text
5
4
3
2
1
0
```

Takšen zapis zanke nam pride prav kadar želimo takoj izvesti kodo v njenem bloku, vendar ni nujno, da se bo ta še kdaj ponovil oziroma se to zgodi le v specifičnih primerih, ki jih določa pogoj.

## `for`

Zanka `for` vrača definiranje pogoja nazaj pred blok zanke, vendar uvaja dodatne dele, ki določajo število izvedb. Oblika zapisa zanke je `dokler (inicializacijski del; pogojni del; izvrševalni del)` oziroma `for (initialization slot; conditional slot; execution slot)`. V delih zanke določimo interval ali število korakov, kolikokrat se blok zanke izvede.

```java
for (int stevec = 0; stevec < 10; stevec++) {
    System.out.println(stevec);
}
```

Potek delovanja zanke `for` najprej izvede inicializacijski del, kjer običajmo nastavimo začetno stanje spremenljivke na katero se opiramo v pogoju. Zatem se izvede pogojni del, ki preveri ustreznost nadaljnjega izvajanja zanke. V kolikor je predpostavka pogoja pravilna, se prične izvajati blok zanke, sicer pa se njeno izvajanje zaključi. V primeru izvedbe bloka, se po zadnjem ukazu v bloku izvede še izvrševalni del, ki običajno zgolj spremeni stanje spremenljivke, ki jo preverjamo v pogoju. Celoten postopek od že opisanega izvajanja pogojnega dela naprej se ponavlja toliko časa, dokler predpostavka pogoja ni več veljavna. Zatem se izvajanje zanke `for` zaključi in program nadaljuje z izvajanjem naslednjih ukazov.

V zgornjem primeru smo na začetku zanke navedli spremenljivko `stevec`, ki določa stanje zanke. Njeno vrednost smo postavili na `0`. Sledi pogojni del, kjer smo zapisali, da želimo števec manjši od `10`. Izvrševalni del po vsakem izvajanju bloka zanke poveča `stevec` za 1. Napisanemu lahko okrajšamo pomen v to, da smo ustvarili zanko, ki blok izvede desetkrat. Tako po zaključku izvajanja programa dobimo naslednji rezultat:

```text
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

Omenimo še, da posamezni deli zanke `for` niso obvezni in jih lahko izpustimo, še vedno pa mora biti pravilen njen zapis (podpičja znotraj oklepajev). Inicializacijski in izrševalni del lahko vsebujeta več stavkov, ki jih izjemoma ločimo z vejico. V kolikor pogojni del pustimo prazen, se ta smatra kot pravilen.

Zapis zanke `for` je veliko bolj kompakten, kot preostali omenjeni zanki, saj vse potrebne stavke za krmiljenje zanke nastavimo v njenih delih.

## Prekinitve

Pogosto se zgodi, da med izvajanjem zanke želimo to zaradi predčasno izpolnjenega cilja prekiniti. To lahko opravimo v času izvajanja bloka, v kateremkoli koraku oziroma iteraciji (za zgornji primer zanke `for` imamo 10 korakov/iteracij). Prekinitev lahko opravimo na dva načina, pri čemer uporabimo sledeči ključni besedi, ki ju moramo obvezno zapisati v blok zanke, kot svoj stavek:

- `continue` - preskočimo izvajanje vseh stavkov napisanih za to ključno besedo in gremo v naslednjo iteracijo izvajanja, če to dovoljuje pogoj
- `break` - na mestu zapisa ključne besede se zanka ustavi, preostali del bloka se ne izvede, temveč se nadaljuje izvajanje ukazov, ki sledijo zanki

```java
for (int stevec = 0;; stevec++) {
    if (stevec % 2 != 0) {
        continue;
    }

    if (stevec > 20) {
        break;
    }

    System.out.println(stevec);
}
```

V zgornjem primeru uporabimo ključno besedo `continue` za nadaljevanje v naslednjo iteracijo, kadar je `stevec` liho število. Podobno ključno besedo `break` uporabimo, ko je `stevec` večji od `20`. Končni rezultat je izpis sodih števil do vključno 20:

```text
0
2
4
6
8
10
12
14
16
18
20
```

## Gnezdenje

Načinu zapisa bloka krmilnega stavka v bloku drugega krmilnega stavka rečemo gnezdenje. Število gnezdenj označimo z nivoji. Gnezdenja se običajno poslužujemo, kadar lahko iz podatkov, ki jih obdelujemo v okviru zanke, pridobimo dodatne podatke, ki so pomembni v tem procesu.

```java
int n = 10;

for (int i = 0; i < n; i++) {
    for (int j = 0; j < n - i - 1; j++) {
        System.out.print(" ");
    }
    for (int j = 0; j < 2 * i + 1; j++) {
        System.out.print("*");
    }
    System.out.println();
}
```

V zgornjem primeru gnezdenje uporabimo dvakrat, v obeh primerih gre za gnezdenje na prvem nivoju. V kolikor bi v katero izmed gnezdenih zank zapisali dodatno zanko, bi s tem imeli gnezdenje na drugem nivoju. Končni rezultat izvajanja tega programa je izris trikotnika:

```text
         *
        ***
       *****
      *******
     *********
    ***********
   *************
  ***************
 *****************
*******************
```
