# Izjeme

V idealnem svetu računalništva bi uporabniki vedno pravilno vnašali podatke v programe, delali z veljavnimi datotekami in nikoli ne bi naleteli na težave izvajanja programov v času njihovega dela. Kot smo večkrat doslej omenili, se moramo tudi pri programiranju držati določenih pravil in konceptov, ki nam dovolijo prevajanje in kasnejše izvajanje kode brez nepredvidenih situacij. Le s takšnim načinom se lahko približamo idealnemu svetu, navkljub temu pa moramo v okviru logike programa pomisliti tudi na situacije, ko uporabniki ne upoštevajo načel uporabe, ki jih predpisuje naš program. Četudi uporabniki ne vpeljejo podatkov ali operacij v program, ki bi lahko vodile v nepredivdeno izvajanje, je delovanje programa še vedno odvisno od ostalih dejavnikov sistema. To pomeni, da moramo tovrstne primere ustrezno obravnavati in uporabniku na nek način sporočiti trenutno stanje programa.

Kadar naletimo na napako v programu, ki ga uporabljamo, je izkušnja popolnoma odvisna od njegovega načina obravnavanja te napake. V tem poglavju bomo spoznali način obravnave napak in njihovo proženje, vrste različnih napak ter možnosti za odpravljanje napak, ki so vezane na nepravilno delovanje logike programa.

## Obravnavanje napak

Predpostavimo, da se med izvajanjem našega programa pojavi napaka. Lahko je povezana z delom z datotekami, mrežno komunikacijo ali bolj osnovnimi težavami, kot sta dostop do napačnega indeksa v tabeli oziroma poskus klica metode na objektu brez dodeljene reference. Običajno pričakujemo, da nam je v vlogi uporabnika stanje programa v času napake sporočeno, program pa sam nekajkrat ponovno poskuša razrešiti nastalo situacijo. Bistveno pri tem je, da program omogoči:

- vračanje v stanje programa, kjer lahko uspešno izvajamo druge operacije,
- shranimo podatke, ki so rezultat naše uporabe programa in uspešno zapustimo program.

Iz vidika razvijalca programa opisan postopek ni nujno enostaven, saj mora biti struktura kode takšna, da lahko napake na ustrezen način ugotovimo in obravnavamo. Za posamezno napako moramo predvideti njeno pojavitev in stanje v katerem bo takrat program, da bomo uporabniku olajšali nadaljnjo interakcijo. Temu primerna mora biti logika programa, ki napako obravnava, zato je pomembno, da se v tem delu zavedamo konteksta in na njegovi podlagi ukrepamo. Nekaj najpogostejših težav s katerimi se srečamo je:

- **Napačno podajanje podatkov s strani uporabnika**: Poleg klasičnih tipkarskih napak, je lahko program uporabljen napačno zaradi nerazumevanja njegovega delovanja. _Primer: Vnos URL naslova spletne strani, pri čemer je napačno naveden naziv protokola. V kolikor tega ne obravnavamo v našem programu, se bo napaka zgodila na omrežnem nivoju._
- **Sistemske napake**: Strojna in programska oprema, ki služita kot osnova za delovanje našega programa, lahko zaradi nepredvidenih situacij deloma odpovesta. _Primer: Nezmožnost komunikacije s tiskalnikom ali iztrošenost tonerja, zaradi česar se tiskanje ne more nadaljevati._
- **Dejanske omejitve**: Strojne ali programske omejitve, ki so na voljo kot sredstva za uporabo v našem programu. _Primer: Zapolnitev prostora na disku/datotečnem sistemu ali poraba celotnega pomnilnika/specifično dodeljene velikosti pomnilnika._
- **Logične in razumske napake**: Rezultat, ki ga pričakujemo po izvedbi programske logike zaradi napačnih operacij v kodi ni ustrezen. _Primer: Koda ne obravnava drugih napak, ki se pojavijo v procesu izvajanja in posledično pride do poskusa dostopa napačnega indeksa tabele ali nebstoječe reference objekta. Napačna uporaba oziroma nerazumevanje delovanja obstoječe programske knjižnice, zaradi česar ta ne deluje kot je predvideno v naši kodi._

Običajen odziv na napako v metodi je vračanje posebne kode napake, na podlagi katere klicoča metoda opravi nadaljnje odločanje o njenem delovanju. Za primer vzemimo metode, ki iz datotek berejo podatke, saj te ponavadi vrnejo vrednost `-1` ob zaključku datoteke, namesto drugega standardnega znaka. Podobno je pri vračanju `null` reference, ki označuje pojav napake v času izvajanja metode. Omenjena načina označevanja sta lahko učinkovita, vendar v določenih primerih premalo natančna. Vedno pa ne moremo vračati kode napake, saj iz rezultata ni mogoče razlikovati med pričakovano vrednostjo in vrednostjo napake. Vrednost `-1` je lahko povsem veljavna v določenem kontekstu, medtem ko v drugem označuje napako. V preteklih poglavjih smo že omenili način, kako se spoprijeti s podatki v programu, ki niso primerni - primer je podajanje `null` reference kot parameter razreda `String` v konstruktor, kjer smo nato s pomočjo metode `Objects.requireNonNull` preprečili nadaljnje izvajanje programa. V tem primeru je šlo za **proženje** _(ang. throwing)_ objekta, ki je vključeval dodatne informacije o napaki. Ob tem metoda ni vrnila nobenega rezultata, temveč ob pojavu napake prenehala z nadaljnjim delovanjem. Pri tem je bilo pričakovano, da se naš program zaključi in nam na standardnem izhodu prikaže opis **izjeme** _(ang. exception)_, ki jo predstavlja objekt z dodatnimi informacijami o napaki. Razlog za prenehanje izvajanja programa je bil v tem, da program ob proženju izjeme išče **obravnavo izjeme** _(ang. exception handler)_, ki zna urediti nastalo situacijo v prid nadaljnjemu izvajanju programa. V našem primeru te obravnave nismo implementirali, zato je tudi prišlo do zaključka izvajanja po pojavu izjeme.

Izjeme imajo lastno sintakso in pripadajo lastni hierarhiji dedovanja. V nadaljevanju bomo spoznali vrste izjem, njihovo sintakso in način njihove obravnave.

## Klasifikacija izjem

V Javi objekti izjem vedno izhajajo iz osnovnega razreda `Throwable`.

```text
                +--------------+
                |              |
                |   Throwable  |
                |              |
                +-------^------+
                        |
       +----------------+----------------+
       |                                 |
+------+-------+                 +-------+------+
|              |                 |              |
|    Error     |                 |   Exception  |
|              |                 |              |
+--------------+                 +-------^------+
                                         |
                               +---------+----------+
                               |                    |
                        +------+-------+    +-------+------+
                        |              |    |              |
                        |  IOException |    |    Runtime   |
                        |              |    |   Exception  |
                        +--------------+    |              |
                                            +--------------+
```

Iz osnovnega razreda `Throwable` takoj izhajata podrazreda `Error` in `Exception`, ki sta namenjena specifičnemu kontekstu napak.

Hierarhija izhajajoča iz podrazreda `Error` opisuje interne napake in situacije, ko pride do izrabe sredstev v okviru izvajalnega sistema Jave. Objektov tega tipa ne prožimo. V primeru, da se v programu pojavi takšna napaka, nam ne preostane drugega, kot da uporabnika obvestimo o težavi in poskušamo končati program brez nadaljnjih napak. Do takšnih situacij ne pride velikokrat.

Hierarhija izhajajoča iz podrazreda `Exception` je pri programiranju v Javi bolj pogosta. Razširja se nadalje v podrazreda:

- `RuntimeException`: Določa napako pri programiranju, ki se proži šele v času izvajanja.
- `IOException`: Določa napako povezano z vhodom in izhodom, zaradi težave pri dostopu do virov ali tokov.

Izjeme, ki razširjajo `RuntimeException` vključujejo težave, kot so:

- Napačna pretvorba _(ang. bad cast)_
- Dostop do indeksa/elementa izven meje _(ang. out-of-bounds access)_
- Dostop do ničelnega kazalnika _(ang. null pointer access)_

Izjeme, ki ne razširjajo `RuntimeException` vključujejo:

- Poskušanje branja datoteke po njenem zaključku
- Poskušanje odpiranja datoteke, ki ne obstaja
- Poskušanje iskanja objekta razreda `Class` za niz, ki označuje neobstoječ razred

Obstaja pravilo "V kolikor gre za `RuntimeException`, je bila napaka narejena v okviru programiranja", ki se običajno izkaže za pravilno. Primer tega je izjema `ArrayIndexOutOfBoundsException`, ki jo lahko obidemo s preverjanjem velikosti tabele, preden poskušamo dostopati do indeksa.  Podobno velja za `NullPointerException`, ki ga lahko obidemo tako, da preverimo ali je vrednost spremenljivke/polja `null`, preden referenciran objekt skušamo uporabiti.

Pri delu z datotekami je nekoliko drugače. Seveda lahko pred odpiranjem datoteke preverimo ali ta obstaja in šele nato operiramo nad njo. Kljub temu se nam lahko zgodi, da je v vmesnem času med preverjanjem in odpiranjem že izbrisana. To pomeni, da je njen obstoj odvisen od okolja in ne samo naše kode. Iz tega naslova še vedno potrebujemo obravnavati izjeme, ki bi se lahko zgodile v povezavi z vhodom in izhodom.

Specifikacija programskega jezika Java označuje vse izjeme, ki izhajajo iz razredov `Error` in `RuntimeException` kot **nepreverjene izjeme** _(ang. unchecked exceptions)_. Vse ostale izjeme označuje kot **preverjene izjeme** _(ang. checked exceptions)_, pri čemer prevajalnik vedno preveri ali zanje zagotavljamo obravnavanje.

### Preverjene izjeme

Metoda lahko proži izjemo v kolikor se v času njenega izvajanja pojavi nepredvidena situacija. Pri tem je prevajalnik seznanjen kakšne vrednosti metoda lahko vrača in kaj točno gre pri izvajanju lahko narobe. Za primer pri branju datotek, program lahko skuša brati iz datoteke, ki ne obstaja ali pa je prazna. Pri tem lahko pride do izjeme `IOException`, ki je deklarirana ob metodi in je z njo seznanjen tudi prevajalnik. Deklaracijo izjeme zapišemo ob metodo ali konstruktor, pred zavite oklepaje, ki označujejo blok. V razredu `java.io.FileInputStream` je deklaracija enega izmed konstruktorjev naslednja:

```java
// ...

public FileInputStream(String name) throws FileNotFoundException
{
    // ...
}

// ...
```

Pri tem za navedbo imena in parametrov metode uporabimo ključno besedo `throws` in dopišemo razred izjeme. Deklaracija v tem primeru označuje, da konstruktor ustvari objekt tipa `FileInputStream`, pri čemer moramo podati en parameter tipa `String`, v primeru napake pa bo metoda prožila izjemo `FileNotFoundException`. V kolikor se napaka zares zgodi, konstruktor ne bo inicializiral novega objekta, temveč bo prožil izjemo objekta `FileNotFoundException`. Za proženjem izjeme izvajalno okolje programa prične z iskanjem bloka za obravnavanje izjeme, ki razume napako iz objekta tipa `FileNotFoundException`.

Pri pisanju lastnih metod v definiciji ne potrebujemo navajati vseh možnih objektov, ki so lahko proženi kot izjema. Za razumevanje kdaj in kaj točno moramo zapisati v definicijo s pomočjo ključne besede `throws`, moramo vedeti, da je izjema prožena v katerikoli naslednji situaciji:

- Ob klicu metode, ki proži preverjeno izjemo - za primer konstruktor razreda `FileInputStream`
- Ko zaznamo napako in prožimo preverjeno izjemo s pomočjo ključne besede `throw`
- Kadar naredimo napako pri programiranju, npr. `tabela[-1] = 1`, kjer se proži nepreverjena izjema (v tem primeru `ArrayIndexOutOfBoundsException`)

V prvih dveh situacijah moramo dopolniti definicijo metode in navesti, da lahko pride do proženja izjem. Razlog je v tem, da morebitno neobravnavanje izjeme lahko privede do širšega problema, ki sega izven konteksta našega programa. Kadar obravnavanje izjem ni prisotno, se trenutni del izvajanja programa prekine. Prav tako lahko v definicijo navedemo več različnih razredov objektov, ki jih pričakujemo kot izjeme.

```java
package io.github.e_gradivo.izjeme;

import java.io.*;

public class BesedilnaDatoteka {
    public String preberi(String ime) throws FileNotFoundException, EOFException {
        // ...
    }
}
```

Pri navajanju razredov izpustimo interne napake, ki so predstavljene z razredom `Error`, saj do njih lahko pride kadarkoli, ne glede na metodo, ki se izvaja. Nad njimi nimamo neposrednega nadzora, zato jih iz navedb izpustimo. Podobno velja tudi za nepreverjene izjeme, ki izhajajo iz razreda `RuntimeException`, le da imamo nad njimi popoln nadzor. Namesto navajanja le teh ob definiciji metode, raje preverimo kako bi do takšnih napak lahko prišlo in jih skušamo odpraviti še preden se pojavijo.

V definicijo metode moramo torej navesti vse preverjene izjeme, ki se lahko zgodijo v času njenega izvajanja. Nad nepreverjenimi izjemami nimamo nadzora (`Error`) ali pa bi jih morali preprečiti sami (`RuntimeException`). Omenimo še, da razredi izjem, ki jih navajamo v definicijo lahko označujejo celotno hierarhijo dedovanja razredov. Za primer spet vzemimo konstruktor `FileInputStream`, ki bi lahko imel v definiciji proženje izjeme `IOException`, namesto `FileNotFoundException`. `FileNotFoundException` je podrazred razreda `IOException`. Razlog za omejitev na podrazred je v tem, da pri uporabi `IOException` ne vemo točno kateri objekt njegovega podrazreda se bo prožil. Lahko bi šlo za splošno izjemo `IOException` ali katerokoli izmed podrazredov, kot je `FileNotFoundException`.

## Proženje izjem

Predpostavimo, da se v času izvajanja poljubne metode `preberiPodatke` zgodi nekaj nepričakovanega. Dolžina namišljene datoteke, ki je bila navedena v zaglavju je 1024 B, dejanski konec pa dosežemo že pri prebranih 512 B. Pri tem se zavedamo, da je nekaj narobe z datoteko ali pa načinom branja, ki ga nad njo izvajamo. Če iz postopka ne moremo ugotoviti kje je prišlo do napake, bomo najverjetneje želeli sprožiti izjemo. Vrsta izjeme za katero se bomo odločali bo zaradi dela z vhodom oziroma izhodom temeljila na razredu `IOException`. Po pregledu dokumentacije programskega jezika Java ugotovimo, da pravzaprav že obstaja razred izjeme, ki ustreza točno temu, kar se je dogodilo v našem primeru. Gre za razred `EOFException`, ki je namenjen sporočanju napak v povezavi z zaključkom datoteke _(ang. end of file)_. Na ustreznem mestu v metodi zato s pomočjo ključne besede `throw` prožimo izjemo:

```java
throw new EOFException();
```

Razred `EOFException` ima poleg praznega še dodaten konstruktor, ki sprejme niz. Vanj je smiselno zapisati nekaj, kar bi nam lahko koristilo v primeru, da bi napako izpisali na standardni izhod.

```java
throw new EOFException("Navedena dolžina datoteke v zaglavju je " + dolzinaDatoteke + "; prebrano: " + dolzinaPrebrano);
```

Proženje izjem je z obstoječimi razredi zelo enostavno. V tem primeru upoštevamo:

- Najdemo ustrezen razred izjeme, ki predstavlja napako
- Ustvarimo objekt tega razreda
- Prožimo objekt

Po proženju izjeme se izvajanje metode prekine in zaradi tega ne potrebujemo vračati kakšnih privzetih vrednosti ali kod napak.

## Ustvarjanje razredov izjem

Napaka, ki se pojavi v logiki programa, ni nujno opisana s kakšnim izmed standardnih razredov izjem. V tem primeru smo primorani sami ustvariti razred, ki opisuje takšno napako. Bistveno pri tem je, da izhaja iz nadrazreda `Exception` ali njegovega podrazreda, kot je na primer `IOException`. Priporočeno je, da ustvarimo tako prazen konstruktor, kot tudi konstruktor, kateremu lahko podamo poljuben niz.

```java
package io.github.e_gradivo.dedovanje;

import java.io.*;

public class PoljubenException extends IOException {
    public PoljubenException() {}
    public PoljubenException(String sporocilo) {
        super(sporocilo);
    }
}
```

V metodi, kjer želimo prožiti izjemo našega razreda, najprej to napovemo v definiciji, nato pa proženje vključimo še v kodo.

```java
// ...

public String preberiPodatke(BufferedReader br) throws PoljubenException {
    // ...
    throw new PoljubenException("Sporočilo o napaki");
    // ...
}

// ...
```

## Prestrezanje izjem

Sedaj vemo, kako prožimo obstoječo ali lastno ustvarjeno izjemo. Postopek je precej enostaven - izjemo sprožimo in nanjo pozabimo. Še vedno pa mora na neki točki v programu obstajati logika, ki to izjemo prestreže in uredi vse potrebno za nadaljnje izvajanje programa ali ustrezen zaključek.

Ob pojavitvi izjeme, ki ni prestrežena, se izvajanje programa zaključi in na standardni izhod izpiše sporočilo, ki pojasnjuje tip izjeme in pripadajoče sledi sklada _(ang. stack trace)_. V izogib privzetemu delovanju, je smiselno izjeme prestreči, kar lahko storimo s `try/catch` blokom. V osnovi ga zapišemo na naslednji način:

```java
try {
    // koda, ki lahko proži izjemo
} catch (FileNotFoundException e) { // navedemo specifično izjemo
    // obravnavamo napako, ki je navedena v objektu imenovanem e
}
```

V kolikor je v kodi znotraj `try` bloka prožena izjema, ki ustreza razredu navedenem v eni izmed `catch` definicij (po zapisu `try` bloka jih lahko navedemo več), potem se zgodi naslednje:

- Program preskoči preostanek kode v `try` bloku
- Program izvede kodo, ki obravnava izjemo in je definirana znotraj ustrezne `catch` definicije, glede na vrsto/razred izjeme

V nasprotnem primeru, če izjema v `try` bloku ni prožena, potem program izpusti izvajanje kode v `catch` blokih. Kadar nobena izmed definicij `catch` ne ustreza vrsti izjeme, ki je bila prožena znotraj `try` bloka, se izvajanje metode nemudoma prekine in v najboljšem primeru, to izjemo obravnava predhodna metoda, v kateri je bil izveden njen klic. Prikažimo napisano še na primeru branja datoteke:

```java
// ...

public void preberi(String datoteka) {
    try {
        InputStream is = new FileInputStream(datoteka);
        int b;
        while ((b = is.read()) != -1) {
            // obdelava prebranega podatka
        }
    } catch (IOException e) {
        e.printStackTrace();
    }
}

// ...
```

Večina kode v `try` bloku je predvidljiva - bere in obdeluje prebrane bajte vse do konca datoteke. Po pregledu dokumentacije za metodo `read` razreda `FileInputStream`, opazimo, da lahko proži izjemo `IOException`. V primeru, da se to res zgodi, se prekine zanka `while`, izvede blok, ki obravnava izjemo `IOException` in kot rezultat obravnave izpiše sledi sklada. Za primer na katerem razložimo delovanje proženja in obravnave izjem, je takšna implementacija zadostna. Obstaja pa še dodatna možnost, ki nam omogoča, da izjemo prenesemo klicatelju. To pomeni, da je ne obravnavamo znotraj naše metode, temveč poleg definicije metode navedemo, da metoda lahko proži izjemo, kar storimo s pomočjo ključne besede `throws`.

```java
// ...

public void preberi(String datoteka) throws IOException {
    InputStream is = new FileInputStream(datoteka);
    int b;
    while ((b = is.read()) != -1) {
        // obdelava prebranega podatka
    }
}

// ...
```

Izpostavimo, da v primeru, ko metoda, ki jo kličemo proži izjemo, prevajalnik pričakuje, da bomo to izjemo prenesli naprej na klicatelja naše metode ali pa jo obravnavali v njej. Kot pravilo upoštevamo, da v kolikor znamo obravnavati proženo izjemo, potem jo dejansko tudi obravnavamo v naši metodi, v nasprotnem primeru pa jo prenesemo na klicočo metodo. Če nismo prepričani ali bo obravnavanje v naši metodi ustrezno, izjemo raje prenesemo. Pri tem obvelja le ena izjema - kadar prepisujemo metodo iz nadrazreda, ki ne proži izjem, potem moramo obravnavati vsako preverjeno izjemo v prepisani metodi. Popravljanje definicije takšne metode za dodajanje ključne besede `throws` oziroma navedbe dodatnih razredov, ki še niso navedeni v metodi nadrazreda, ni dovoljeno.

### Prestrezanje več izjem

Pri prestrezanju več izjem, ki se lahko pojavijo v bloku `try`, obravnavamo vsako izmed njih bolj specifično. Za vsak možen razred, ki predstavlja izjemo, zapišemo svojo definicijo `catch` in v njen blok ustrezno obravnavo:

```java
try {
    // koda, ki lahko proži izjeme
} catch (FileNotFoundException e) {
    // obravnava za primer, ko datoteka ne obstaja
} catch (UnknownHostException e) {
    // obravnava za primer, ko gostitelj ni znan
} catch (IOException e) {
    // obravnava za primer ostalih težav z vhodom/izhodom
}
```

Objekt izjeme običajno vsebuje več informacij o napaki, ki se je zgodila tekom izvajanja. Pri tem se lahko zanesemo na sporočilo, ki ga vsebuje objekt ...

```java
e.getMessage()
```

... ali pa pridobimo dejansko vrsto/razred izjeme:

```java
e.getClass().getName()
```

Poleg zaporedne obravnave posameznih izjem lahko v Javi združimo več različnih izjem v eno definicijo bloka `catch`. Funkcionalnost nam pride prav le kadar vrste/razredi izjem niso podrazredi en drugemu.

```java
try {
    // koda, ki lahko proži izjeme
} catch (FileNotFoundException | UnknownHostException e) {
    // obravnava za primer, ko datoteka ne obstaja ali ni znan gostitelj
} catch (IOException e) {
    // obravnava za primer ostalih težav z vhodom/izhodom
}
```

### Ponovno proženje in veriženje izjem

Izjeme smemo prožiti tudi v bloku `catch`. Običajno to storimo, ko želimo spremeniti vrsto/razred izjeme. V kolikor ustvarimo lastno knjižnico, ki jo uporabljajo tudi drugi razvijalci, je smiselno, da vse izjeme, ki ne izhajajo neposredno iz naše kode, uokvirimo v lasten vmesni razred. Primer razreda takšne izjeme je `ServletException`. Uokvirja napake, ki se zgodijo v času obdelave strežniškega zahtevka.

```java
try {
    // dostopamo do baze
} catch (SQLException e) {
    throw new ServletException("napaka podatkovne baze: " + e.getMessage());
}
```

V primeru opazimo, da v sporočilo naše izjeme `ServletException` zapišemo razlog napake in dodamo še sporočilo iz izjeme, ki jo obravnavamo. Boljši način je, da namesto vključevanja sporočila obravnavane izjeme, raje podamo v konstruktor `ServletException` referenco na to izjemo.

```java
try {
    // dostopamo do baze
} catch (SQLException e) {
    throw new ServletException("napaka podatkovne baze", e);
}
```

Ob prestrezanju izjeme `ServletException` nato lahko pridobimo tudi izvorno izjemo, ki je povzročila obravnavo:

```java
try {
    // koda, ki proži ServletException
} catch (ServletException e) {
    // ...
    Throwable izvornaIzjema = e.getRootCause();
}
```

To tehniko imenujemo ovijanje _(ang. wrapping)_ in je zelo priporočljiva. Omogoča nam, da v lastni knjižnici ovijemo izvorne izjeme in na njihovi osnovi razvijalcu omogočimo, da sprejme boljše odločitve pri implementaciji obravnavanja izjem. Ovijanje lahko uporabimo tudi pri proženju preverjene izjeme v metodi, ki ji ni dovoljeno prožiti takšne izjeme. S prestrezanjem preverjene izjeme le-to lahko ovijemo v izjemo v času izvajanja _(ang. runtime exception)_.

Včasih želimo izjemo prestreči v namen beleženja napake, nato pa jo ponovno prožiti brez kakršnekoli spremembe. To storimo kot doslej, le da namesto ustvarjanja novega objekta izjeme, obstoječo izjemo še enkrat prožimo.

```java
try {
    // dostopamo do baze
} catch (SQLException e) {
    // opravimo shranjevanje napake iz izjeme v na primer datoteko
    throw e;
}
```

### Blok `finally`

Ob proženju izjeme se izvajanje preostale kode v metodi preneha, na koncu pa se po obravnavi metoda še zaključi. Problem nastane v primeru, da je metoda zaklenila dostop do lokalnega vira, s čimer upravlja le ona. V primeru, da je med uporabo vira prišlo do izjeme, mora biti ta vir sproščen, saj bo sicer ostal zaklenjen. Ena izmed rešitev je, da v takšni metodi prestrežemo vse izjeme, odklenemo dostop do vira in nato še enkrat prožimo presteženo izjemo. Takšen pristop ni najboljši, saj moramo v tem primeru na dveh mestih upravljati z odklepanjem dostopa do vira - v primeru uspešne izvedbe kode in v primeru proženja izjeme. Blok `finally` nam omogoča, da izvedemo ta del programske logike ne glede na to ali je vmes prišlo do izjeme ali ni.

```java
// ...

public void preberi(String datoteka) {
    InputStream is = new FileInputStream(datoteka);
    try {
        // 1.
        // koda, ki lahko proži izjemo
        // 2.
    } catch (IOException e) {
        // 3.
        // obravnavanje izjeme v povezavi z vhodom/izhodom
        // 4.
    } finally {
        // 5.
        is.close();
    }
    // 6.
}

// ...
```

Glede na podan primer si oglejmo tri možne situacije v katerih se bo izvedel blok `finally`:

1. Koda ne proži izjem. V tem primeru program najprej izvede vso kodo znotraj bloka `try` in zatem še blok `finally`. Zatem se pričnejo izvajati ukazi za celotnim `try-catch-finally` blokom. Povzeto po točkah se izvedejo: 1., 2., 5. in 6.
2. V kodi se pojavi izjema (v tem primeru `IOException`), ki jo prestreže blok `catch`. Izvede se vsa koda v bloku `try`, dokler ni prožena izjema. Preostala koda v bloku je izpuščena, prične pa se izvajati blok `catch`, ki ima v definiciji naveden ustrezen razred izjeme (v tem primer `IOException`). Zatem se izvede še koda v bloku `finally`. V kolikor obravnava v bloku `catch` ne proži znova obstoječe ali nove izjeme, se izvajanje programa nadaljuje za celotnim `try-catch-finally` blokom. Povzeto po točkah, se izvedejo: 1., 3., 4., 5. in 6. V primeru, da blok `catch` proži izjemo, je izvajanje po točkah naslednje: 1., 3. in 5.
3. Koda proži izjemo, ki ni zajeta v nobeni izmed `catch` definicij. Koda v bloku `try` se izvaja do ukaza, zaradi katerega se proži izjema. Preostala koda v bloku je izpuščena, zatem pa se takoj izvede blok `finally`. Izjema je prenešena na klicočo metodo. Povzeto po točkah se izvedeta le 1. in 5.

Blok `finally` lahko uporabljamo tudi brez navedbe blokov `catch`.

```java
// ...

public void preberi(String datoteka) {
    InputStream is = new FileInputStream(datoteka);
    try {
        // koda, ki lahko proži izjemo
    } finally {
        is.close();
    }
}

// ...
```

Ukaz `is.close()` v bloku `finally` se izvede ne glede na to, ali se v bloku `try` pojavi izjema ali ne. V primeru, da se, se samodejno proži ponovno in mora biti obravnavana v drugem bloku `catch`.

```java
// ...

public void preberi(String datoteka) {
    InputStream is = new FileInputStream(datoteka);
    try {
        try {
            // koda, ki lahko proži izjemo
        } finally {
            is.close();
        }
    } catch (IOException e) {
        // obravnava za primer ostalih težav z vhodom/izhodom
    }
}

// ...
```

Notranji blok `try` ima v tem primeru zgolj eno nalogo - zagotoviti, da bo vhodni tok zaprt. Zunanji blok `try` ima prav tako zgolj eno nalogo - zagotoviti, da so napake ustrezno obravnavane. Takšen pristop ni samo bolj jasen, temveč tudi bolj funkcionalen - morebitne napake oziroma izjeme v notranjem bloku `finally` so prestrežene v zunanjem bloku.

Opozorimo še na morebitno težavo pri uporabi bloka `finally`, kadar imamo v njem vračanje rezultata s pomočjo ključne besede `return`. V primeru, da v bloku `try` že uporabimo `return`, se pred dejanskim vračanjem tega rezultata izvede še blok `finally`. Rezultat, ki se dejansko vrne pa ostaja pri zadnjem bloku `finally`, saj se ta tudi nazadnje izvede.

```java
// ...

public static int pretvoriStevilo(String s) {
    try {
        return Integer.parseInt(s);
    } finally {
        return 0; // napaka
    }
}

// ...
```

V primeru klica metode iz primera `pretvoriStevilo("50")`, blok `try` vrne celoštevilski rezultat `50`. Zatem se izvede še blok `finally`, ki vrača celoštevilski rezultat `0`. Glede na to, da je zadnji del kode, ki se izvede v bloku `finally`, je njegov rezultat tudi končni rezultat, ki ga vrne metoda.

V primeru novega klica `prevtoriStevilo("nic")`, se po klicu metode `Integer.parseInt` proži izjema `NumberFormatException`. V tem primeru se zgolj izvede še blok `finally`, ki vrne lasten rezultat, izjema pa pri tem ni obravnavana. To lahko privede do nepričakovanega izvajanja programa.

Blok `finally` je namenjen zapiranju virov ali zaključevanju drugih sredstev in ne spremembi dejanske programske logike. Posledično v njem ne navajamo ukazov, ki spremenijo način delovanja programa (`return`, `throw`, `break`, `continue`).

### Izjeme pri delu z viri

Situacije, ko za dokončanje določenih logičnih operacij v programu potrebujemo delati z viri, so zelo pogoste. V ta namen v Javi obstaja vmesnik `AutoCloseable`, ki zahteva implementacijo metode `close`, ta pa klicoči metodi prenaša morebitno izjemo vrhnjega razreda `Exception`. S pomočjo bloka `try` lahko vire, ki implementirajo ta vmesnik, definiramo neposredno v njegovo definicijo:

```java
try (Resource res = ...) {
    // obdelava vira res
}
```

Ob zaključku izvajanja kode v bloku `try`, se metoda `close` na viru pokliče samodejno. Tipičen primer z dejansko kodo je naslednji:

```java
try (Scanner is = new Scanner(new FileInputStream("/pot/do/datoteke", StandardCharsets.UTF_8))) {
    while (is.hasNext()) {
        System.out.println(is.next());
    }
}
```

Ob zaključku izvajanja bloka `try` ali ob proženju izjeme v času izvajanja, je metoda `is.close()` klicana samodejno. Način delovanja je enakovreden navedbi blokov `try` in `finally`. V definiciji bloka `try` smemo navesti tudi več različnih virov, ki jih ločimo s podpičjem.

```java
try (
    Scanner is = new Scanner(new FileInputStream("/pot/do/datoteke", StandardCharsets.UTF_8));
    PrintWriter pw = new PrintWriter("/pot/do/datoteke2", StandardCharsets.UTF_8)
) {
    while (is.hasNext()) {
        pw.println(is.next().toUpperCase());
    }
}
```

Ne glede na zaključek izvajanja bloka `try`, se zatem na obeh objektih `is` in `pw` kliče metoda `close`. V kolikor ne bi uporabljali definicije virov v bloku `try`, bi poleg tega morali uporabiti še blok `finally`.

Poleg deklaracije in inicializacije objekta vira v definiciji bloka `try`, lahko namesto tega uporabimo tudi obstoječo končno spremenljivko, ki jo v definiciji le navedemo.

```java
// ...

public static void izpisiVse(String[] vrstice, PrintWriter pw) {
    try (pw) { // uporabimo končno spremenljivko
        for (String vrstica : vrstice) {
            pw.println(vrstica);
        }
    } // ob zaključku bloka se izvede pw.close()
}

// ...
```

Težava pri pristopu z definicijo virov v bloku `try` je le, kadar se proži izjema tako v bloku, kot tudi ob klicu metode `close` na viru. Implementacija bloka `try` s takšno definicjo nastalo situacijo uredi tako, da izvorno izjemo proži ponovno, druga izjema, ki izhaja iz metode `close`, pa je označena kot nenadzorovana izjema _(ang. suppressed exception)_. Ta je obravnavana samodejno in je vključena v izvorno izjemo s pomočjo klica metode `addSuppressed`. V kolikor v takšnih situacijah želimo dostopati do nenadzorovane izjeme, lahko nad izvorno kličemo metodo `getSuppressed`.

Kadar delamo z viri je tako najbolj smiselno uporabiti blok `try`, kjer jih navedemo v njegovi definiciji. Pri takšnem bloku lahko prav tako uporabimo tudi bloka `catch` in `finally`, ki se izvedeta za klicem metode `close` na virih.

## Nasveti za uporabo izjem

Pri uporabi izjem med razvijalci prihaja do različnih mnenj o tem kdaj je potrebno prožiti izjeme in na katerih mestih jih je primerno uporabiti. Za lažje sprejemanje odločitev o tem si pomagamo z naslednjimi nasveti.

### Obravnavanje izjem ni zamenjava za enostavno testiranje

Za primer lahko vzamemo program, ki poskuša deset milijonkrat vzeti _(ang. pop)_ element iz praznega sklada _(ang. stack)_. Najprej to stori z ugotavljanjem, če je sklad prazen:

```java
if (!sklad.empty()) {
    sklad.pop();
}
```

Zatem pa ločeno ne glede na rezultat nadaljnjega izvajanja metode `pop` poskušamo vzeti element iz sklada ter pri tem obravnavamo razred izjeme `EmptyStackException`, ki nas opozarja, da operacije ne moremo izvesti.

```java
try {
    sklad.pop();
} catch (EmptyStackException e) {
    // blok brez ukazov (noop)
}
```

Primerjava med obemi različicami programa se izkaže v tem, da je klic metode `empty` v prvem primeru veliko hitrejši, kot poskušanje s prestrezanjem izjeme. Iz tega naredimo zaključek, da je izjeme smiselno uporabljati v izjemnih situacijah in ne za vsako ceno.

### Izogibanje preveč podrobnemu obravnavanju izjem

Mnogo razvijalcev poskuša vsak ukaz, ki lahko proži izjemo oviti v svoj blok `try`.

```java
PrintStream ps;
Stack sklad;
for (int i = 0; i < 20; i++) {
    try {
        int element = sklad.pop();
    } catch (EmptyStackException e) {
        // obravnava praznega sklada
    }

    try {
        ps.writeInt(element);
    } catch (IOException) {
        // obravnava napake pri pisanju
    }
}
```

Takšen pristop oteži branje kode. Na logiko programa raje pogledamo celovito in skušamo zajeti del logike v skupen blok `try`. Bistvo programa iz primera je, da iz sklada pridobi zadnjih 20 elementov in jih zapiše v datoteko. V kolikor se pri pridobivanju elementa iz sklada ali pisanju elementa v datoteko pojavi napaka, nanjo pri posamezni obravnavi ukaza ne moremo precej drugače vplivati, kot bi s skupnim zapisom v en blok `try`. Prav tako je to smiselneje, saj verjetno želimo odnehati z obdelavo podatkov takoj, ko se pojavi napaka.

```java
try {
    for (int i = 0; i < 20; i++) {
        int element = sklad.pop();
        ps.writeInt(element);
    }
} catch (IOException e) {
    // obravnava napake pri pisanju
} catch (EmptyStackException e) {
    // obravnava praznega sklada
}
```

S popravkom primera vidimo, da se berljivost kode precej izboljša, hkrati pa ločimo obdelavo podatkov od obravnave napak.

### Ustvarjanje smiselne hierarhije izjem

Pri proženju izjeme moramo najti ustrezen razred, ki bo predstavljal napako. V kolikor ta ni na voljo, je najbolje ustvariti lastnega. Pri tem upoštevamo tudi to, da namesto tega ne prožimo enostavno izjeme `RuntimeException` ali pa le prestežemo razred `Throwable`. V obeh primerih je koda težko razumljiva, saj ne poznamo konteksta, ki ga s tem nadrazredom obravnavamo. Posledično je oteženo tudi vzdrževanje takšne kode.

Spoštovati moramo razliko med preverjenimi in nepreverjenimi izjemami. Preverjene izjeme povzročijo precej težav, zato jih ne prožimo za logične napake programa.

Prožene izjeme je smiselno oviti v druge izjeme, ki bolje predstavljajo kontekst v katerem se zgodijo. Za primer, ko razčlenjujemo število iz datoteke, prestrežemo izjemo `NumberFormatException` in jo ovijemo v `IOException` ali `NasaKnjiznicaException`.

### Izogibanje neobravnavanju izjem

Kadar uporabljamo metode, ki v definiciji navajajo proženje izjem, nas prevajalnik ob morebitnem neobravnavanju vedno opozarja, da moramo navedene izjeme nujno obravnavati. Problem lahko enostavno rešimo tako, da v definicijo naše metode zapišemo prenos izjem naprej. Kljub temu bomo na neki točki še vedno morali obravnavati te izjeme, zato se včasih najenostavneje zdi, da izjeme samo obravnavamo z definicijo, brez dejanske logike:

```java
// ...

public void preberi(String datoteka) {
    try {
        // koda, ki lahko proži izjemo
    } catch (Exception e) {
        // blok brez ukazov (noop)
    }
}

// ...
```

S takšnim načinom se bo koda prevedla in bo delovala, razen takrat ko se zares pojavi izjema. V takšnih primerih bodo napake zgolj izpuščene, kar pa lahko kritično vpliva na nadaljnje izvajanje programa. Iz tega razloga se takšnega pristopa ne poslužujemo, temveč vedno obravnvamo napake tako, da do njih ne more priti ponovno oziroma ustrezno spremenijo nadaljnje delovanje programa.

### Predčasno zaznavanje napak

Pri zaznavanju napak ob napačno podanih parametrih metodi, se občasno pojavi vprašanje, če ne bi bilo morda bolje le vrniti neke privzete vrednosti, kot prožiti izjemo. Za primer - ali mora metoda `Stack.pop` vrniti vrednost `null` ali prožiti izjemo, kadar je sklad prazen? Najverjetneje je bolje, če proži izjemo `EmptyStackException` v času pojavitve napake, kot da zaradi uporabe vrednosti, ki ne kaže na obstoječi objekt naletimo na `NullPointerException` kasneje, ko želimo ta objekt uporabiti.

### Prenos izjem na klicočo metodo

Prestrezanje vseh proženih izjem je včasih težko, saj mogoče ne poznamo dovolj konteksta v katerem se te pojavijo. Pri prestrezanju izjem za konstruktor razreda `FileInputStream` ali njegove metode `readLine`, najprej pomislimo na prestrezanje izjem, ki se lahko zgodijo v času izvajanja te kode. Včasih je celo bolje, če teh izjem ne prestrezamo in jih raje prenesemo na klicočo metodo:

```java
// ...

public void preberi(String datoteka) throws IOException {
    InputStream is = new FileInputStream(datoteka, StandardCharsets.UTF_8);
    // ...
}

// ...
```

Metode, ki kličejo takšne metode, kot je navedena v primeru, imajo včasih na voljo boljše tehnike obvladovanja napak in obveščanja uporabnika o nastalih težavah.
