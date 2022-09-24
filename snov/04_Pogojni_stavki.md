# Pogojni stavki

Izvajanje programa določajo krmilni konstrukti, ki so namenjeni definiranju ustreznega obnašanja na podlagi podatkov in programske logike. En izmed njih je tudi pogojni stavek, ki določa kdaj se izvede določen blok kode.

## Sklop bloka

V preteklem poglavju smo spoznali bloke in spremenljivke ter omenili njihov namen. Za razumevanje krmilnih konstruktov, moramo najprej spoznati tudi dodatne omejitve, ki jih vpeljujejo bloki. Spremenljivke smo doslej vedno navedli znotraj glavnega bloka programa in do njih prav tako dostopali v istem bloku. Pri krmilnih konstruktih pa bomo poleg njihove navedbe dopisali še dodatne bloke, ki so namenjeni pogojnemu izvajanju.

Lokalnost spremenljivk določa, iz kje lahko do njih dostopamo, omejitev pa določimo z bloki. Velja pravilo, da so vse spremenljivke iz vrhnjih blokov dostopne v gnezdenih blokih.

## Pogoji

S pogoji se ukvarjamo, kadar želimo izvesti specifičen del kode v primeru izpolnitve določene predpostavke. Pogojni stavek v Javi zapišemo kot `če (pogoj) stavek` oziroma `if (condition) statement`. Poenostavljeno napisano, če je pogoj izpolnjen, naj se izvede stavek v nadaljevanju. Tipično po izpolnitvi pogoja želimo izvesti več stavkov, zaradi česar se znova opremo na bloke in uporabimo sledeč zapis.

```java
if (condition) // če je pogoj izpolnjen
{
    statement1; // izvedi 1. stavek
    statement2; // izvedi 2. stavek

    // ...
}
```

V primeru dejanske kode in z uporabo spremenljivk:

```java
int kolicina = 5;
int dovoljenaKolicina = 10;
String stanje = "V obdelavi";
boolean dovoliNadaljevanje = false;

if (kolicina <= dovoljenaKolicina) {
    stanje = "Uspešno";
    dovoliNadaljevanje = true;
}
```

Za izpolnitev pogoja v kodi, mora biti `kolicina` manjša ali enaka vrednosti spremenljivke `dovoljenaKolicina`. Kadar to drži, se `stanje` nastavi kot uspešno ter `dovoliNadaljevanje`, na katerega se lahko zanašamo v nadaljevanju programa.

Način podajanja pogoja za izvedbo mora biti vedno tak, da je njegov rezultat izražen v logični obliki (podatkovni tip `boolean`). Pri tem si pomagamo s pogojnimi operatorji. Veljavni vrednosti znotraj oklepajev pogojnega stavka sta torej lahko samo `true` ali `false`.

## Operatorji

Z operatorji sestavimo izraz, ki nato privede do rezultata v logični obliki. Pogojni stavek je lahko sestavljen iz več različnih pogojev (izrazov), ki določajo končno pravilnost. Operatorji omogočijo pretvorbo podatkov poljubne oblike v binarno vrednost `true` ali `false`.

Osnovni pogojni operatorji, ki nam omogočajo primerjavo veličin so:

| Operacija        | Operator | Primer                  |
| ---------------- | -------- | ----------------------- |
| Enakost          | `==`     | `4 % 2 == 0` => `true`  |
| Neenakost        | `!=`     | `4 % 2 != 0` => `false` |
| Večje            | `>`      | `5 > 5` => `false`      |
| Večje ali enako  | `>=`     | `5 >= 5` => `true`      |
| Manjše           | `<`      | `5 < 3` => `false`      |
| Manjše ali enako | `<=`     | `5 <= 3` => `false`     |

Za sestavljanje zahtevnejših pogojev, potrebujemo še dva operatorja:

| Operacija | Operator | Primer                     |
| --------- | -------- | -------------------------- |
| In (and)  | `&&`     | `true && false` => `false` |
| Ali (or)  | `\|\|`   | `true \|\| false` => `true`  |

## Vejitve

Osnovni pogojni stavek `če (pogoj) stavek` nam omogoča izvedbo stavka le kadar je pogoj pravilen. Običajno logika programa vključuje dodatne primere, ki jih stavek prvotnega pogoja ne zajema, zato namesto uporabe ločenega pogojnega stavka uporabimo vejitve.

```java
if (kolicina <= dovoljenaKolicina) {
    stanje = "Uspešno";
    dovoliNadaljevanje = true;
} else {
    stanje = "Neuspešno";
    dovoliNadaljevanje = false;
}
```

Poleg stavka `if` smo sedaj dodali še stavek `else`, ki se izvede v primeru, da podani pogoj ni veljaven. To pomeni, da se v enem pogojnem stavku izvede točno ena vejitev, bodisi `if` ali `else`.

Vedno pa ne obstajata samo pravilna in nepravilna trditev, temveč še vmesne trditve, ki spadajo med njiju.

```java
int minimalnaKolicina = 3;
int minimalnaKolicinaPopust = 7;

if (kolicina >= minimalnaKolicinaPopust && kolicina <= dovoljenaKolicina) {
    stanje = "Uspešno (+popust)";
    dovoliNadaljevanje = true;
} else if (kolicina >= minimalnaKolicina && kolicina <= dovoljenaKolicina) {
    stanje = "Uspešno";
    dovoliNadaljevanje = true;
} else if (kolicina >= 0 && kolicina <= minimalnaKolicina) {
    stanje = "Neveljavno";
    dovoliNadaljevanje = false;
} else {
    stanje = "Neuspešno";
    dovoliNadaljevanje = false;
}
```

Vmesne trditve izrazimo s stavki `else if`, ki preverjajo delne predpostavke. Pravilnost pogojev se izvaja od vrha navzdol in prekine takoj, ko se izpolni prvi veljaven pogoj ali pa dosežemo stavek `else`. Po izpolnitvi pogoja se nemudoma pričnejo izvajati stavki v njegovem bloku.

## Vejitve okrajšano

Kadar obstajata zgolj pravilna in nepravilna trditev, si lahko pomagamo z okrajšano različico vejitve:

```java
String obvestilo = dovoliNadaljevanje
    ? "Pravilno ste vnesli količino, zato lahko nadaljujete."
    : "Pri vnosu količine je prišlo do napake, prosim popravite podatek.";
```

Oblika okrajšave je sestavljena po modelu: `<pogoj> ? <true> : <false>`.

Na tem mestu velja opomba o dobri praksi, ki pravi, da okrajšano različico uporabljamo previdno in le v primerih enostavnejših pogojnih stavkov. Kadar pišemo zahtevnejše, predvsem daljše pogojne stavke, je zaradi preglednosti kode smiselneje zapisati pogojni stavek v prvotni obliki z blokom.

## Stikalo

Poleg enostavne pogojne vejitve obstaja še dodatna stikalna _(ang. switch)_ vejitev. Njena uporaba je smiselna, kadar imamo večje število vmesnih trditev ali možnosti, kjer pogojni stavek lahko postane nepregleden. Bistvena razlika med pogojnim in stikalnim stavkom je v načinu primerjave. Pogojni stavek vpeljuje operatorje s katerimi preverimo ustreznost dveh podatkov, dočim stikalni stavek primerja le enakost prvega podatka z vsemi ostalimi.

Kot parameter stikalu podamo spremenljivko, ki mora biti podatkovnega tipa `byte`, `short`, `char`, `int` ali `String`. Ta tvori osnovo, s katero se kasneje primerjajo vse možnosti. Vsako izmed možnosti navedemo s pomočjo stavka `case`, v katerega podamo stavke, ki se izvedejo v primeru enakosti (tako kot blok pri pogojnem stavku). V kolikor vemo, da v določenih primerih nobena izmed podanih možnosti ne bo enaka, lahko podamo privzeti stavek `default`. Za zaključek izvajanja stavkov moramo na koncu navesti ključno besedo `break`, s katero preprečimo nadaljnje izvajanje preostale kode v nadaljevanju.

```java
int stMeseca = 6;
String mesec;

switch (stMeseca) {
    case 1:
        mesec = "januar";
        break;
    case 2:
        mesec = "februar";
        break;
    case 3:
        mesec = "marec";
        break;
    case 4:
        mesec = "april";
        break;
    case 5:
        mesec = "maj";
        break;
    case 6:
        mesec = "junij";
        break;
    case 7:
        mesec = "julij";
        break;
    case 8:
        mesec = "avgust";
        break;
    case 9:
        mesec = "september";
        break;
    case 10:
        mesec = "oktober";
        break;
    case 11:
        mesec = "november";
        break;
    case 12:
        mesec = "december";
        break;
    default:
        mesec = "?";
        break;
}
```

V primeru, da v stavku pri kateri izmed možnosti navedeni v stavku `case` izpustimo ključno besedo `break`, se pričnejo izvajati stavki za možnost, ki sledi trenutni (vse dokler ne doseže ključne besede za prekinitev `break`).
