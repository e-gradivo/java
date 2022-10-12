# Bloki in spremenljivke

Pri pisanju kode moramo upoštevati pravila sintakse programskega jezika, eno izmed ključnih je uporaba blokov. Poleg tega v njihovem okviru za začasno shranjevanje rezultatov operacij v kodi uporabljamo spremenljivke.

## Bloki

Java za razčlenjevanje posameznih delov programa zahteva zapis blokov, ki jih označimo z zavitim oklepajem `{` in zaklepajem `}`. Na primeru kode prvega programa ...

```java
class PozdravljenSvet {
    public static void main(String[] args) {
        System.out.println("Pozdravljen, svet!");
    }
}
```

... opazimo dva bloka. Prvi je namenjen uokvirjanju kode gradnika programa `PozdravljenSvet`, drugi pa naslednjemu gradniku `main`. V tem primeru je drugi gradnik gnezden v prvem. Na takšen način določimo hierarhijo gradnikov v programu, kar nam pomaga pri sklicevanju na vsakega izmed njih. Zaviti oklepaj predstavlja začetek gradnika, zaklepaj pa njegov zaključek. V primeru bloka `main` smo vanj zapisali tudi ukaz `System.out.println("Pozdravljen, svet!");`, bistveni poudarek pa je tukaj na zadnjemu ločilu, ki ima posebno vlogo. Podpičje `;` namreč zaključuje posamezen stavek ali ukaz v bloku, kar omogoča prevajalniku prepoznavanje naslednjega ukaza.

Omenimo še način uporabe gradnika `System.out.println`. Nanj se sklicujemo s pomočjo navadnih oklepajev `()`, ki pa ne označujejo bloka, temveč so namenjeni izvedbi klica tega gradnika. Pri zapisu `System.out.println("Pozdravljen, svet!");` v oklepaje podamo še parameter, v tem primeru `"Pozdravljen, svet!"`, ki označuje niz z določeno vrednostjo. Po zaključku klica gradnika s podpičjem govorimo o ukazu. Klic gradnika oziroma izvedba ukaza sprožita izvajanje kode, ki je navedena v podanem gradniku. Pri izvajanju programa se ukazi v bloku izvajajo zaporedno, kot so navedeni v kodi. To pomeni, da se pri klicu drugega gradnika najprej izvede njegova koda, šele nato se nadaljuje prvotna.

```java
class PozdravljenSvet {
    public static void main(String[] args) {
        System.out.print("Pozdravljen, "); // z izvedbo tega ukaza se na izhod izpiše samo "Pozdravljen, "
        System.out.print("svet"); // po izvedbi tega ukaza, na izhodu vidimo izpisano "Pozdravljen, svet"
        System.out.println("!"); // po izvedbi tega ukaza, na izhodu vidimo izpisano "Pozdravljen, svet!"
    }
}
```

V zgornjem primeru izpišemo niz `Pozdravljen, svet!` po delih. V kolikor katerikoli ukaz izbrišemo ali pa spremenimo njihov vrstni red, končni izpis ne bo več enak.

## Spremenljivke

Konstrukt programskega jezika, ki omogoča shranjevanje vrednosti v programu pod določenim imenom, imenujemo spremenljvka. Tekom izvajanja programa se vrednost spremenljivke lahko spreminja, ni pa nujno.

### Deklaracija

Java je statično tipiziran programski jezik, kar pomeni, da moramo vsaki spremenljivki določiti ustrezen podatkovni tip. To storimo tako, da pred njeno ime zapišemo enega izmed podatkovnih tipov, ki bo ustrezno zajemal nabor vrednosti, ki jih lahko določimo tej spremenljivki.

```java
double rezultatRacuna;
int steviloOseb;
long prebivalcevZemlje;
boolean koncano;
```

Z zapisom podatkovnega tipa, imena spremenljivke in na koncu podpičja, govorimo o deklaraciji spremenljivke. Z deklaracijo v programu navedemo njen obstoj in možnost uporabe v nadaljevanju kode. Podpičje ob koncu navedbe tipa in imena spremenljivke označuje, da gre za stavek kode, ki se nato v času izvajanja programa tudi izvede v tem obsegu.

Pri poimenovanju spremenljivk moramo začeti s črkami, pri čemer je končno zaporedje ne glede na nadaljnji zapis lahko sestavljeno tako iz črk, kot številk. Pri črkah omenimo le še to, da so v Javi te izjemoma določene kot:

- razpon črk abecede od `'A'` do `'Z'` oziroma od `'a'` do `'z'`
- znak `'_'` in `'$'`
- katerikoli Unicode znak, ki je določen kot črka abecede izbranega jezika

Glede na omenjeno smejo imena spremenljivk vsebovati tudi šumnike, vendar tako iz zgodovinskih razlogov, kot tudi pogostosti pojavitve v kodi, njihovo uporabo odsvetujemo. Izpostaviti je potrebno še, da so imena občutljiva na velikost črk, kar pomeni, da sta spremenljivki ...

```java
int steviloOseb;
int stevilooseb;
```

... različni in gre v tem primeru dejansko za deklaracijo dveh spremenljivk. V kolikor želimo novi spremenljivki določiti ime že obstoječe, nas bo prevajalnik opozoril, da je bila spremenljivka s takšnim imenom že predhodno deklarirana in preprečil nadaljnje prevajanje. Poimenovanjem spremenljivk, ki imajo samo drugačno velikost črke, se naj skušamo pri lastnih programih izogniti, saj lahko hitro pride do napačne uporabe in v drugem kontekstu, kot je bilo prvotno predvideno.

Pri poimenovanju je potrebno upoštevati še, da uporaba znaka `'$'` v naši kodi ni priporočena, saj je ta namenjen zgolj imenom  ustvarjenim s strani prevajalnika in ostalih orodij, ki so del JDK.

### Inicializacija

Deklaraciji sledi eksplicitna inicializacija v smislu prirejanja vrednosti spremenljivki. Spremenljivke ne moremo uporabljati, dokler ji ne nastavimo vrednosti (je neinicializirana), na kar nas sicer opozori tudi prevajalnik.

```java
int steviloOseb;
System.out.println(steviloOseb);
```

Pri prevajanju kode iz zgornjega primera naletimo na napako, ...

```text
Spremenljivke.java:24: error: variable steviloOseb might not have been initialized
        System.out.println(steviloOseb);
                           ^
1 error
```

ki nam sporoča, da spremenljivka `steviloOseb` najverjetneje ni bila inicializirana. Težavo odpravimo tako, da spremenljivki s pomočjo znaka enakosti (=) priredimo primerno vrednost.

```java
int steviloOseb;
steviloOseb = 5;
```

V okviru inicializacije spremenljivki torej priredimo določeno vrednost, kar nam omogoči, da jo smemo v nadaljnji kodi tudi uporabiti. Vse spremenljivke na katere se v kodi navezujemo, morajo biti pred dejansko uporabo tako deklarirane, kot inicializirane.

### Definicija

Z deklaracijo v programu napovemo obstoj določene spremenljivke, z inicializacijo pa ji priredimo vrednost. Oba dela smo doslej pisali ločeno. Najprej smo zapisali deklaracijo, kjer smo navedli podatkovni tip in ime spremenljivke. Zatem smo zapisali še inicializacijo, kjer smo navedli ime spremenljivke, znak enakosti in neko vrednost. V izogib takšnemu načinu pisanja, smemo to poenostaviti tako, da zapišemo vse skupaj v enem stavku. Temu rečemo definicija spremenljivke.

```java
int steviloOseb = 5;
```

S tem prihranimo vrstico kode, vendar takšen način zapisa ni vedno mogoč. Kadar v času deklaracije ne poznamo vrednosti spremenljivke, moramo še vedno uporabljati ločen zapis za deklaracijo in inicializacijo.

Omenimo še, da specifikacija programskega jezika Java ne navaja definicije kot strokovni izraz, ki ga uporabljamo pri poimenovanju tovrstnih operacij v kodi. Termin definicije je tako pogost zaradi ostalih programskih jezikov, kjer se uporablja, da ga kljub temu omenjamo tukaj v takšni obliki.

## Konstante

V nasprotju s spremenljivkam, ki jim lahko tekom izvajanja programa spreminjamo vrednost, moramo omeniti še konstante. Bistvena razlika med njima je v tem, da smemo nad konstantami izvesti le enkratno inicializacijo oziroma prirejanje. Zapis konstant je enak spremenljivkam, le da pred podatkovni tip dodamo še ključno besedo `final`.

```java
final int STEVILO_OSEB = 5;
```

Pri poimenovanju se držimo pravila, da vse črke zapišemo z veliko, ločilo med posameznimi besedamo pa je podčrtaj. Alternativni način zapisa konstant je z ločeno deklaracijo in inicializacijo, pri čemer moramo biti pozorni, da konstanti ne poskušamo še enkrat spremeniti vrednosti.

```java
final int STEVILO_OSEB;
STEVILO_OSEB = 5;
```

V kolikor navkljub opravljeni inicializaciji, konstanti želimo prirediti novo vrednost, nas o tem opozori prevajalnik in prekine nadaljnje prevajanje.

```text
Spremenljivke.java:27: error: cannot assign a value to final variable STEVILO_OSEB
        STEVILO_OSEB = 3;
        ^
1 error
```

### Konvencija poimenovanja

Spremenljivke se po dogovoru pišejo z malimi črkami ter veliko začetnico vseh besed, razen prve. Takšen zapis imenujemo camelCase. Nekaj primerov:

- visina
- telesnaVisina
- rezultat
- rezultatIzracuna
- steviloSprememb

Konstante se po dogovoru pišejo z velikimi črkami, besede pa ločimo s podčrtajem. Takšen zapis imenujemo SCREAMING_SNAKE_CASE. Nekaj primerov:

- STEVILO_PI
- PRIVZETA_VREDNOST
- NAJVEC_SPREMEMB
- DOVOLJENI_ZNAKI
- STEVILO_PRESTAV

## Operacije

Cilj izvajanja operacij je sestavljanje vrednosti iz vhodnih podatkov. V nadaljevanju bomo spoznali širok nabor aritmetičnih in bitnih operacij, ki jih lahko opravimo v programskem jeziku Java.

### Aritmetične

Operacije, ki jih lahko izvajamo nad podatki številskega tipa zajemajo vse običajne matematične operacije - seštevanje, odštevanje, množenje in deljenje, poleg tega pa še operacijo modulo, ki vrne ostanek po deljenju števila. Vrstni red upoštevanja operatorjev je enak kot v matematiki, če to želimo spremeniti pa ustrezno uporabimo oklepaje. Operator modulo je enakovreden množenju in deljenju.

| Operacija  | Izraz | Primer    |
| ---------- | ----- | --------- |
| Seštevanje | a + b | 2 + 3 = 5 |
| Odštevanje | a - b | 3 - 2 = 1 |
| Množenje   | a * b | 2 * 3 = 6 |
| Deljenje   | a / b | 4 / 2 = 2 |
| Modulo     | a % b | 8 % 3 = 2 |

Deljenje celih števil z 0 povzroči napako v programu, ista operacija pri delu z decimalnimi števili pa vrne vrednost neskončnosti oziroma NaN. Tip končnega rezultata po izvedbi operacije je odvisen od tipa vhodnih podatkov. Vedno zavzame bolj natančno izmed vhodnih, torej če je eno decimalno število, bo izhod tudi decimalno število.

```java
int a = 7;
int b = 3;
int c;

c = a + b; // c = 9
c = a - b; // c = 4
c = a * b; // c = 21
c = a / b; // c = 2 (uporabljamo cela števila)
c = a % b; // c = 1 (ostanek)

double d;

d = a / 2.0; // d = 3.5
d = a / b;   // d = 2.0
```

Pri delu z enim glavnim številskim podatkom in ostalimi pomožnimi, lahko izkoristimo krajši zapis operacij nad spremenljivko. To storimo tako, da glavni podatek shranimo v spremenljivko, ostale pa uporabimo potem z operacijami neposredno nad njo.

```java
int a = 7;

// Običajni zapis
a = a + 3;
a = a - 2;
a = a * 5;
a = a / 2;
a = a % 4;

// Krajši zapis
a += 3;
a -= 2;
a *= 6;
a /= 4;
a %= 8;
```

Pri krajšemu zapisu moramo biti pozorni na ustrezno umestitev operatorja, ki ga vedno napišemo pred znak enakosti.

Za izvajanje operacij seštevanja in odštevanja nad celimi števili obstaja dodaten krajši zapis, ki nam omogoča povečevanje ali zmanjševanje vrednosti za 1.

```java
int a = 5;

// Povečevanje vrednosti
a++; // a = 6
++a; // a = 7

// Zmanjševanje vrednosti
a--; // a = 6
--a; // a = 5
```

Kadar uporabimo tovrstne operatorje govorimo o operaciji inkrementacije ali dekrementacije. Posebej moramo biti pozorni na čas izvedbe povečevanja/zmanjševanja vrednosti, ki je odvisna od lokacije kamor umestimo operator. V kolikor se ta pojavi pred imenom spremenljivke, je njena vrednost spremenjena že v isti vrstici. V nasprotnem primeru, kadar je operator za imenom, pa je sprememba vrednosti spremenljivke opravljena šele po zaključku izvajanja vrstice in spremenjena vrednost vidna v vseh naslednjih vrsticah.

```java
int a = 5;
int b = 15;

int c = 2 * a++; // c = 10
int d = c * ++b; // d = 160
int e = a * b;   // e = 6 * 16 = 96
```

### Bitne

V kolikor želimo delati neposredno na nivoju bitov, potrebujemo temu primerne operacije. Java vključuje vse glavne operatorje, ki omogočajo izvajanje operacij nad biti. Pri zapisu števil si pomagamo z dvojiškim številskim sistemom, kar pomeni, da pred dejansko dvojiško vrednostjo dodamo predpono `0b`, na primer `0b0011`.

| Operacija        | Zapis   | Primer              |
| ---------------- | ------- | ------------------- |
| Pomik levo       | a << b  | 1011 << 1 = 0110    |
| Pomik desno      | a >> b  | 1011 >> 1 = 1101    |
| Log. pomik desno | a >>> b | 1011 >>> 1 = 0101   |
| Negacija         | ~a      | ~1011 = 0100        |
| In               | a & b   | 1011 & 0110 = 0010  |
| Ali              | a \| b  | 1010 \| 1100 = 1110 |
| Ekskluzivni ali  | a ^ b   | 1011 ^ 1101 = 0110  |

```java
int a = 0b0111; // a = 7
int b = 0b0011; // b = 3

int c = a & b; // c = 3 (0b0011)
int d = a | b; // d = 7 (0b0111)
int e = a ^ b; // e = 4 (0b0100)
```

## Komentarji

V času programiranja pogosto implementiramo programsko logiko, ki je običajno s prvim pregledom ne razumemo v celoti ali pa se izvaja na zelo specifičen način. Pri tem lahko v namen lažjega razumevanja ob posamezne dele kode zapišemo komentarje, ki obrazložijo način njenega delovanja. S tem pomagamo drugim razvijalcem, ki prebirajo našo kodo ali v primeru, da dlje časa ne nadgrajujemo oziroma vzdržujemo programa, tudi sebi ob ponovnem pregledu prihranimo čas. Komentarji so v času prevajanja prezrti in ne vplivajo na preostalo kodo in način izvajanja programa.

Java podpira tri načine označevanja komentarjev:

1. Dve poševnici `//` - ko v vrstico kode zapišemo dve poševnici, se preostanek kode v tej vrstici tretira kot komentar.

    ```java
    System.out.println("Pozdravljen, svet!"); // to je komentar
    ```

2. Poševnica in zvezdica `/* */` - kadar želimo bolj natančno označiti komentar ali pa je ta zapisan v več zaporednih vrsticah, uporabimo komentar s poševnico in zvezdico.

    ```java
    System.out.print("Pozdravljen, ");
    /*System.out.print("uporabnik. ");
    System.out.print("To je ");
    System.out.print("programerski ");*/
    System.out.print("svet" /* vmesni komentar */);
    System.out.println("!");
    ```

3. Dokumentacija `/** */` - pri dokumentiranju gradnikov programa uporabimo komentar podoben poševnici in zvezdici, vendar ima ta pri začetnem zapisu dve zvezdici. V času generiranja dokumentacije se upoštevajo le tovrstni komentarji, ki morajo biti umeščeni pred ustrezne gradnike kode.

    ```java
    /**
    * Program za izpis pozdrava svetu.
    * @version 1.0 2022-09-01
    * @author E-gradivo
    */
    class PozdravljenSvet {
        public static void main(String[] args) {
            System.out.println("Pozdravljen, svet!");
        }
    }
    ```

Način uporabe komentarjev je povsem poljuben, med razvijalci pa obstaja dogovorjena oblika le-teh. Govorimo o dveh vrstah komentarjev:

- vsebinskih
- tehničnih

Vsebinski komentarji so namenjeni opisovanju funkcionalnosti kode, kot smo to navedli v začetku tega podpoglavja. Izpostavimo le pravilo dobre prakse, ki pravi - v kolikor konstrukti programskega jezika dovolj dobro opišejo rezultat izvajanja kode, dodajanje komentarjev ni potrebno. Posledično se zdi smiselno dodajati komentarje le tam, kjer smo prepričani, da bodo nam ali ostalim razvijalcem zares prišli prav. V nasprotnem primeru lahko komentarji postanejo moteči in celo otežijo prebiranje kode.

S komentarji si lahko v času razvoja programa pomagamo še tako, da vanje zapišemo na čem trenutno delamo ali podamo predvidene zahteve, ki jih mora program izpolnjevati. Tovrstni komentarji so tehnične narave. Sčasoma jih pobrišemo, saj so namenjeni lastni uporabi in sledenju napredka. Občasno v kodi najdemo tudi kakšen komentar oblike ...

```java
// TODO: Popravi v naslednji različici
```

..., namenjen razvijalcem, ki nadgrajujejo funkcionalnost naslednje različice programa. Če sami tvorimo takšen komentar, je smiselno zapisati tudi podrobnosti kaj točno je potrebno popraviti. V primeru, da bo to namesto nas takrat popravljal nekdo drug, bo to zagotovo opravil precej hitreje, kot če bo sprva moral odkriti na kaj se ta komentar v resnici sploh nanaša.

## Interakcija s konzolo

Za pripravo dinamičnih programov, kjer vhodne podatke pridobimo s strani uporabnika, bomo spoznali način interakcije s konzolo. Osnovni programi, ki smo jih napisali doslej, so imeli podatke zapisane neposredno v kodi, kar pomeni, da bi morali za vsak drugačen izračun pripraviti svoj program s pravimi podatki. To seveda ni smiselno, saj ne moremo v naprej predvideti vseh možnih podatkov, ki jih bodo uporabniki podali v program. Interakcija s konzolo poteka na isti način, kot smo to videli pri uporabi interaktivne jezikovne lupine.

### Izhod

Preden se lotimo branja uporabniških podatkov, bomo morali uporabniku sporočiti kakšne vrste podatek nas zanima. V ta namen bomo spoznali dva osnovna ukaza - pisanje na izhod ter pisanje na izhod pri čemer se izpiše še nova vrstica. Izhod je v primeru konzole okrajšava za standardni izhod _(ang. standard output)_, ki pomeni pisanje v okvir vrhnjega procesa, od koder smo naš program zagnali.

Za enostaven izpis na standardni izhod uporabimo ukaz `System.out.print` ...

```java
System.out.print("Moj program V");
System.out.print(1.5);
System.out.print(" | ");
System.out.print("Vnesi poljubno število: ");
```

pri čemer se na izhodu v konzoli izpiše naslednje besedilo:

```text
Moj program V1.5 | Vnesi poljubno število:
```

Kot vidimo, klici ukazov izpišejo podatke neposredno v isto vrstico. V izogib temu, lahko uporabimo ukaz `System.out.println` ...

```java
System.out.print("Moj program V");
System.out.print(1.5);
System.out.println();
System.out.println("----------------");
System.out.println();
System.out.print("Vnesi poljubno število: ");
```

... pri čemer se na izhodu v konzoli izpiše naslednje besedilo:

```text
Moj program V1.5
----------------

Vnesi poljubno število:
```

Kot parameter ukazoma `System.out.print` in `System.out.println` smemo podati tudi spremenljivko. Podobno temu lahko pri izpisu niza uporabimo operator združevanja `+`, ki deluje nad nizi in omogoča sestavljanje dveh podatkov v en niz. Več o tem pa v poglavju o nizih.

```java
final double VERZIJA_PROGRAMA = 1.5;
System.out.print("Moj program V");
System.out.print(VERZIJA_PROGRAMA);

int najljubsaStevilka = 7;
System.out.println("Moja najljubša številka: " + najljubsaStevilka);
```

### Vhod

Za razliko od pisanja podatkov na standardni izhod, za branje potrebujemo nekaj več vrstic kode, ki nam sploh omogočijo prejem uporabniškega vnosa. Pri tem si pomagamo z obstoječim gradnikom, ki je na voljo v standardni knjižnici, imenovanim `Scanner`. Ta nam omogoča branje iz standardnega vhoda _(ang. standard input)_, ki nam omogoča prejem podatkov poslanih preko vrhnjega procesa iz katerega smo naš program zagnali. Za začetek moramo ustvariti nov gradnik `Scanner`, preko katerega nato zajemamo podatke, ki jih vnese uporabnik.

```java
import java.util.Scanner;

class UporabniskiProgram {
    public static void main(String[] args) {
        Scanner in = new Scanner(System.in);
        System.out.print("Vnesite poljubno besedo: ");
        String beseda = in.next();

        System.out.println("---------");
        System.out.println("Vaša poljubna beseda: " + beseda);
    }
}
```

V zgornjem primeru najprej opazimo prvo vrstico kode, ki se začne z `import java.util.Scanner;`. Ta del v našo kodo doda sklic na gradnik `Scanner`, ki se nahaja na navedeni poti. Če želimo v nadaljevanju programa uporabljati gradnik, je dodajanje sklica obvezno, saj sicer prevajalnik ne ve na katerega izmed gradnikov se sklicujemo. Zatem v glavnem delu programa ustvarimo nov gradnik `Scanner`, ki mu kot parameter podamo standardni vhod `System.in` - `Scanner in = new Scanner(System.in);`. Kasneje izpišemo besedilo, ki uporabniku pove kakšen podatek od njega pričakujemo. Za branje iz vhoda uporabimo ukaz `in.nextLine()`, ki prebere niz iz vhoda ter ga nato shrani v spremenljivko `beseda` - `String beseda = in.nextLine();`. Program pred nadaljevanjem čaka na uporabniški vhod in dokler tega uporabnik ne zaključi s potrditveno tipko (enter), se tudi ne izvaja dalje. Po uspešnem vnosu podatka in potrditvi se izvajanje nadaljuje in s tem tudi izpišejo preostali podatki na izhod.

Pri branju s pomočjo gradnika `Scanner` lahko pridobimo podatke tudi v drugih podatkovnih tipih, doslej smo prikazali samo primer za niz. V spodnji tabeli je seznam vseh podprtih podatkovnih tipov in pripadajočih ukazov, ki nam vrnejo podatke (v kolikor so tudi pravilno podani na vhodu) v pričakovani obliki. Pri ukazu se sklicujemo na ustvarjen gradnik `in`.

| Podatkovni tip | Ukaz             | Opomba                                              |
| -------------- | ---------------- | --------------------------------------------------- |
| byte           | in.nextByte()    | /                                                   |
| short          | in.nextShort()   | /                                                   |
| int            | in.nextInt()     | /                                                   |
| long           | in.nextLong()    | /                                                   |
| float          | in.nextFloat()   | /                                                   |
| double         | in.nextDouble()  | /                                                   |
| boolean        | in.nextBoolean() | /                                                   |
| String         | in.next()        | vrne zaporedje znakov (niz) vse do prvega presledka |
| String         | in.nextLine()    | vrne niz celotne vrstice do potrditve               |

Omenimo še, da podatkovni tip `char` ni podprt neposredno, saj kot rezultat za znakovni vhod vedno pridobimo niz, iz katerega lahko pridobimo posamezen znak (več o tem v poglavju o nizih).
