# Vhod in izhod

Osnovo za delo in komunikacijo z računalnikom tvori koncept vhoda in izhoda _(ang. input/output)_, ki je poleg okvira strojne opreme uporabljen tudi v programski opremi. Ne glede na področje strojne ali programske opreme je bistvo koncepta možnost prenosa signala ali podatkovnega toka od enega vmesnika (oddajnika) do drugega (sprejemnika). V tem poglavju naredimo pregled vhoda in izhoda v okviru programskega jezika Java in zmožnosti shranjevanja ter branja podatkovnega toka. Ta nam omogoča delo z datotekami, v katere shranjujemo podatke ali stanje v katerem se trenutno nahaja program. Za boljše strukturiranje datotek si ogledamo še gradnike, ki nam omogočajo delo z mapami.

## Podatkovni tokovi

Ločimo med različnimi podatkovnimi tokovi, ki jih uporabljamo glede na tip zapisa podatkov.

### Bajtni tokovi _(ang. byte streams)_

Zapis podatkov v programih običajno predstavimo z zbirko podatkovnega tipa `byte`, v kateri se nahaja zaporedje bajtov oziroma jih vanjo zapisujemo. Z njimi operiramo pri dveh ključnih operacijah, branju in pisanju. Java v ta namen uvaja koncept vhodno-izhodnih tokov _(ang. input/output streams)_, ki omogočajo učinkovito prenašanje podatkov od izvora do ponora. Za branje uporabljamo **vhodni tok** _(ang. input stream)_, za pisanje pa **izhodni tok** _(ang. output stream)_. Z operacijama branja in pisanja zgolj določimo smer v katero potujejo podatki, nad njima pa moramo zato definirati še vmesnik, ki določa kontekst v katerem to izvajamo. Lahko gre za delo z datotekami, omrežnimi povezavami ali celo pomnilniškimi bloki. Glede na to, da vsak izmed kontekstov uvaja lasten protokol delovanja, Java v standardni knjižnici vključuje abstraktna razreda `java.io.InputStream` in `java.io.OutputStream`. S tem nas na nivoju bajtov (podatki), branja in pisanja (operacije), kontekst ne zanima več, saj je ključnega pomena zgolj to, da razredi, ki jih napišemo v podporo logiki konteksta, pravilno implementirajo zahtevane metode iz razširjenih abstraktnih razredov.

### Znakovni tokovi _(ang. character streams)_

Navkljub možnosti branja in pisanja bajtov, obstaja možnost, da podatki, ki jih želimo predstaviti potrebujejo več prostora za njihovo shranjevanje. Primer takšnih podatkov so znakovne oziroma besedilne informacije, ki so predstavljene z lastnim kodiranjem _(ang. encoding)_, običajno v standardu Unicode. Implementacija standarda UTF-8 določa velikost posameznega znaka oziroma kodne enote _(ang. code point)_, ki je lahko od enega bajta, pa vse do štirih bajtov, pri čemer pogostejši znaki uporabljajo manj bajtov. UTF-16, ki je uporabljen v okviru podatkovnega tipa `char` je določen z eno ali dvemi kodnimi enotami, kjer posamezna zaseda dva bajta (oziroma 16 bitov). Posledično moramo za operaciji branja in pisanja uporabljati drugačno implementacijo, ki omogoča pravilen zapis znakov podanega kodiranja. Temu sta namenjena abstraktna razreda `java.io.Reader` in `java.io.Writer`, ki temeljita na dvobajtnih `char` vrednostih, namesto predhodno omenjene vrednosti `byte`.

## Branje in pisanje bajtov

Abstraktni razred `InputStream` zahteva implementacijo metode:

```java
abstract int read()
```

Njen namen je branje enega bajta in vračanje njegove vrednosti. V primeru zaključka vhodnega vira, mora vrniti vrednost `-1`. Implementacija je odvisna od konteksta pri katerem se izvaja branje. Pri razredu `FileInputStream` metoda bere en bajt iz datoteke. Pri uporabi statičnega končnega polja `System.in` metoda bere iz standardnega vhoda, ki ga predstavlja vhod konzole ali preusmerjene datoteke. Razred `InputStream` implementira metodo za branje tabele bajtov ter metodo, ki omogoča izpuščanje določenega števila bajtov. Poleg ostalih vključuje še dve bolj pomembni metodi `available` in `close`.

Abstraktni razred `OutputStream` zahteva implementacijo metode:

```java
abstract void write(int b)
```

Njen namen je zapisovanje enega bajta na izhod. Implementacija je prav tako odvisna od kontektsa v katerem se izvaja pisanje. Pri razredu `FileOutputStream` metoda zapisuje en bajt v datoteko, pri čemer v ozadju implementacije upošteva dodajanje podatka na konec datoteke ali pa zapis na začetek. Pri uporabi statičnega končnega polja `System.out` metoda piše na standardni izhod, ki ga predstavlja izhod konzole ali preusmerjene datoteke. Razred `OutputStream` vključuje še dve prazni metodi `flush` in `close`, ki se uporabljata pri shranjevanju in zapiranju datoteke po zaključku pisanja.

Metodi `read` in `write` blokirata nadaljnje izvajanje programa, dokler bajt ni dejansko prebran ali zapisan. To pomeni, da kadar do vhodnega ali izhodnega toka ne moremo takoj dostopati (običajno zaradi zasedenosti omrežne povezave), bo trenuten del programa v katerem smo, blokiral nadaljnje izvajanje ukazov, ki se pojavljajo v njegovi metodi ali širšem sklopu. Pri branju si lahko pomagamo s klicanjem metode `available`, ki nam vrne število bajtov, ki jih lahko preberemo brez blokiranja pred naslednjim klicem na tem toku.

```java
package io.github.e_gradivo.vhodizhod;

import java.io.*;

public class BajtiBranje {
    public static void main(String[] args) throws IOException {
        InputStream f = new FileInputStream("datoteka.txt");
        int steviloBajtov = f.available();
        if (steviloBajtov > 0) {
            byte[] podatki = new byte[steviloBajtov];
            f.read(podatki);
        }
        f.close();
    }
}
```

Ob zaključku branja ali pisanja na vhodni/izhodni tok, ga moramo vedno zapreti s pomočjo metode `close`. Ta klic sprosti vsa sredstva operacijskega sistema, ki so vezana na odprto navezujočo se datoteko, saj v povezavi s tem obstajajo določene omejitve. V kolikor ima program odprtih preveč tokov datotek oziroma jih po zaključku dela z njimi ne zapre, lahko pride do dosega ali prekoračitve omejitev, zaradi česar program preneha funkcionirati. Ob zapiranju izhodnega toka se _izplakne_ _(ang. flushes)_ vse bajte, ki so bili zapisani predhodno, vendar so čakali v medpomnilniku za shranjevanje večjega števila bajtov (razlog za hranjenje zapisanih bajtov v medpomnilniku je preprečevanje shranjevanja manjšega števila podatkov na disk, kar ob pogostih izvajanjih lahko vpliva na njegovo učinkovitost). Posledično v primeru, da toka ne zapremo lahko pride do zastoja zadnjih zapisanih bajtov v medpomnilniku, ki pa niso nikoli izplaknjeni in tako pride do izgube dela podatkov. Obstaja tudi možnost ročnega izplakovanja podatkov s pomočjo klica metode `flush`.

Kljub temu, da razreda za vhodni oziroma izhodni tok zagotavljata metode za delo z branjem `read` in pisanjem `write`, ju razvijalci uporabljajo poredko, z izjemo kadar je potrebno uveljaviti logiko operacij v okviru nekega novega konteksta. Podatki s katerimi običajno delamo so predstavljeni s številkami, nizi in objekti, ne neposredno bajti. Iz tega razloga potem raje uporabimo razrede, ki že razširjajo `InputStream` in `OutputStream` ter omogočajo neposredno pridobivanje podatkov v obliki, ki jo želimo v programu neposredno interpretirati.

## Besedilni vhod in izhod

Delo z besedilom zahteva uporabo znakovnih kodiranj _(ang. character encoding)_. Java interno uporablja standard UTF-16, pogosto pa se uporablja tudi standard UTF-8. Poglejmo si vrednosti nizov in njihovih kodiranj na primerih.

| standard | niz | kodiranje (v šestnajstiškem zapisu) |
| -- | -- | -- |
| UTF-16 | Java | 00 4a 00 61 00 76 00 61 |
| UTF-8 | Java | 4a 61 76 61 |
| -- | -- | -- |
| UTF-16 | Kodiranje | 00 4b 00 6f 00 64 00 69 00 72 00 61 00 6e 00 6a 00 65 |
| UTF-8 | Kodiranje | 4b 6f 64 69 72 61 6e 6a 65 |
| -- | -- | -- |
| UTF-16 | Šola | 01 60 00 6f 00 6c 00 61 |
| UTF-8 | Šola | c5 a0 6f 6c 61 |

Naredimo primerjavo med nizoma _Java_ in _Šola_ in se osredotočimo na kodiranje po [standardu UTF-8](https://en.wikipedia.org/wiki/UTF-8#Codepage_layout). Ugotovimo, da prvi niz za zapis potrebuje štiri bajte, drugi niz pa pet, čeprav sta oba sestavljena iz štirih znakov. Poglejmo si še posamezne črke, kjer se prvi začne z `J`, drugi pa s `Š`. Tu je tudi bistvena razlika, iz katere je razvidno zakaj drugi niz potrebuje pet bajtov. `Š` je šumnik, ki se v znakovnem kodiranju nahaja bolj oddaljeno in posledično njegova kodna enota za zapis potrebuje več bajtov. V okviru standarda UTF-16 za isti primer vidimo, da se namesto ničelnega prvega bajta (primer za `Java`) ta spremeni v dejansko vrednost (primer za `Šola`).

Za delo z besedilom obstaja kontekstualna implementacija abstraktnih razredov `Reader` in `Writer`, ki ju po namenu uporabe lahko enačimo z razredoma `InputStream` in `OutputStream`. Za branje besedilnih podatkov uporabljamo razred `InputStreamReader`, za zapisovanje pa `OutputStreamWriter`. Implementacija razredov še vedno deluje na nivoju bajtov, le da pri branju izbrano zaporedje bajtov primerja s kodnimi enotami, pri pisanju pa kodne enote pretvarja v bajte.

Branje iz standardnega vhoda naredimo na naslednji način ...

```java
package io.github.e_gradivo.vhodizhod;

import java.io.*;

public class BesedilniVhod {
    public static void main(String[] args) throws IOException {
        Reader r = new InputStreamReader(System.in);
        System.out.println(r.read()); // izpiše kodno enoto prve črke v decimalni obliki
        r.close();
    }
}
```

... pri čemer `InputStreamReader` prevzame znakovno kodiranje gostujočega sistema. Pri tem gre lahko za starejša kodiranja, kot sta Windows 1252 ali MacRoman. Iz tega razloga v konstruktorju vedno podamo standardno znakovno kodiranje s pomočjo konstant iz razreda `java.nio.charset.StandardCharsets`.

```java
package io.github.e_gradivo.vhodizhod;

import java.io.*;
import java.nio.charset.StandardCharsets;

public class BesedilniDatoteka {
    public static void main(String[] args) throws IOException {
        Reader r = new InputStreamReader(new FileInputStream("datoteka.txt"), StandardCharsets.UTF_8);
        if (r.ready()) {
            System.out.println(r.read()); // izpiše kodno enoto prve črke datoteke v decimalni obliki
        }
        r.close();
    }
}
```

### Pisanje

Shranjevanje besedilnih podatkov opravimo s pomočjo razreda `PrintWriter`, ki nadgrajuje logiko abstraktnega razreda `Writer`. Namesto zapisovanja posamezne kodne enote, ki se pretvori v bajte, ima prijaznejši vmesnik, ki nam je znan že iz izpisa na standardni izhod preko statičnega objekta `System.out`. To pomeni, da lahko uporabljamo metode `print`, `println` in `printf`, ki sprejmejo vrednosti podane v različnih podatkovnih tipih - števila, znake, logične vrednosti, nize in objekte.

```java
PrintWriter pw = new PrintWriter(
    new OutputStreamWriter(
        new FileOutputStream("besedilo.txt"), StandardCharsets.UTF_8
    )
);
// ali podprta okrajšana različica prejšnjega zapisa
PrintWriter pw2 = new PrintWriter("besedilo.txt", StandardCharsets.UTF_8.toString());
```

Pri uporabi razreda `PrintWriter` moramo biti pozorni na izplakovanje podatkov, ki se sicer privzeto hranijo v medpomnilniku. V kolikor bi želeli neposredno zapisovanje na končno lokacijo (npr. v datoteko), moramo nastaviti logično vrednost polja `autoFlush` na `true`. To lahko storimo pri klicu konstruktorja, ki kot parameter najprej sprejme izhodni tok, nato pa na mesto drugega parametra navedemo vrednost `true`.

```java
PrintWriter pw = new PrintWriter(
    new OutputStreamWriter(
        new FileOutputStream("besedilo.txt"), StandardCharsets.UTF_8
    ),
    true // nastavimo neposredno izplakovanje podatkov
);
```

Klici metod za izpis `print` ne vračajo izjem, zato moramo po zaključku s pomočjo metode `checkError` preveriti ali je v procesu izpisa morda prišlo do napake.

```java
package io.github.e_gradivo.vhodizhod;

import java.io.*;
import java.nio.charset.StandardCharsets;

public class BesedilniPisanje {
    public static void main(String[] args) throws IOException {
        PrintWriter pw = new PrintWriter("besedilo.txt", StandardCharsets.UTF_8.toString());
        pw.print("Pozdravljen, ");
        pw.println("svet! 1234567890");
        pw.print("--");
        pw.println();
        pw.println("nova vrstica");
        if (pw.checkError()) {
            // pri izpisu je prišlo do napake, ukrepamo na ustrezen način
        }
        pw.close();
    }
}
```

### Branje

Pridobivanje shranjenih podatkov besedilne oblike nam omogoča razred `BufferedReader`, ki nadgrajuje logiko abstraktnega razreda `Reader`. Namesto branja zaporedja bajtov, ki predstavljajo določeno kodno enoto, ima prijaznejši vmesnik preko katerega lahko beremo celotno vrstico s pomočjo metode `readLine`.

```java
package io.github.e_gradivo.vhodizhod;

import java.io.*;
import java.nio.charset.StandardCharsets;

public class BesedilniBranje {
    public static void main(String[] args) throws IOException {
        InputStream is = new FileInputStream("besedilo.txt");
        BufferedReader br = new BufferedReader(
            new InputStreamReader(is, StandardCharsets.UTF_8)
        );
        if (br.ready()) {
            String vrstica = null;
            while ((vrstica = br.readLine()) != null) {
                System.out.println(vrstica);
            }
        }
        br.close();
    }
}
```

Za branje lahko uporabimo tudi razred `Scanner`, preko katerega smo v preteklosti opravljali branje uporabniških vnosov iz standardnega vhoda.

```java
package io.github.e_gradivo.vhodizhod;

import java.io.*;
import java.nio.charset.StandardCharsets;
import java.util.Scanner;

public class BesedilniRazclenjevanje {
    public static void main(String[] args) throws IOException {
        InputStream is = new FileInputStream("besedilo.txt");
        Scanner scn = new Scanner(
            new InputStreamReader(is, StandardCharsets.UTF_8)
        );
        while (scn.hasNextLine()) {
            System.out.println(scn.nextLine());
        }
        scn.close();
    }
}
```

Bistvena razlika med razredoma `BufferedReader` in `Scanner` je v načinu branja vhoda. `BufferedReader` je namenjen zgolj branju znakovnih podatkov in posledično optimiziran za učinkovito delo z znakovnim tokom. `Scanner` je prvotno namenjen razčlenjevanju podatkov, ki jih dobi na vhod in zaradi tega v primerjavi z razredom `BufferedReader` ni tako učinkovit, saj primarno ni namenjen izključno delu z znakovnimi tokovi. Razčlenjevanje, ki ga implementira `Scanner` nam omogoča, da podatke takoj pretvori v ustrezen podatkovni tip. To pomeni, da v kolikor imamo datoteko z vrsticami, kjer se nahajajo samo števila, lahko enostavno kličemo metodo `nextInt` in pridobimo število v pravilnem podatkovnem tipu.

```java
package io.github.e_gradivo.vhodizhod;

import java.io.*;
import java.nio.charset.StandardCharsets;
import java.util.Scanner;

public class BesedilniRazclenjevanje {
    public static void main(String[] args) throws IOException {
        InputStream is = new FileInputStream("stevila.txt");
        Scanner scn = new Scanner(is);
        while (scn.hasNextInt()) {
            System.out.println(scn.nextInt());
        }
        scn.close();
    }
}
```

## Delo z datotekami

Pristopa k branju in pisanju s pomočjo vhodnih in izhodnih tokov smo prikazali na primeru bajtnih in znakovnih tokov. V okviru primerov smo že vključili razrede, ki omogočajo delo z datotekami in opravili osnovni operaciji v tem kontekstu. Kljub temu pa zgolj branje in pisanje ne določata končnega nabora operacij, ki pripomorejo pri delu z datotekami. Vključiti moramo še druge operacije, ki omogočajo celovito delo z datotečnim sistemom.

### Poti

Pot določimo z zaporedjem imen map, ki jim lahko sledi še celotno ime datoteke s končnico. Celotna pot in njeni deli so odvisni od platforme na kateri jo definiramo, zato se tega držimo tudi pri razvoju našega programa. Prvi del poti predstavlja korenski del, kot je `/` (Unix) ali `C:\` (Windows). V okviru Unixa se zaporedje imen map ločuje s pomočjo poševnice `/`, v okviru Windowsa pa s pomočjo povratne poševnice `\`. Za primer mape imenovane `Program` v korenskem imeniku sta poti naslednji:

- Unix: `/Program`
- Windows: `C:\Program`

Pot, ki jo začnemo s korenskim delom je **absolutna**, v kolikor pa se navezujemo na podmapo iz trenutne lokacije, pa je pot **relativna**.

```java
package io.github.e_gradivo.vhodizhod;

import java.nio.file.Path;
import java.nio.file.Paths;

public class Poti {
    public static void main(String[] args) {
        Path absolutna = Paths.get("/home", "jan");
        Path relativna = Paths.get("io", "github", "e_gradivo");

        System.out.println(absolutna); // izpiše /home/jan
        System.out.println(relativna); // izpiše io/github/e_gradivo
    }
}
```

Za določanje poti uporabimo razred `java.nio.file.Paths` z metodo `get`, za hranjenje pa razred `java.nio.file.Path`. Pot, ki se hrani v objektu ni nujno obstoječa, saj smemo hraniti tudi poti, ki jih bomo ustvarili v prihodnje oziroma le želimo preveriti, če obstajajo.

### Branje in pisanje datotek

Razred `java.nio.file.Files` nam omogoča hitro izvajanje pogostih datotečnih operacij. Celotno vsebino datoteke lahko preberemo z metodo `readAllBytes`:

```java
Path pot = Paths.get("io", "github", "e_gradivo", "besedilo.txt");
byte[] bajti = Files.readAllBytes(pot);

// spremenimo bajte v niz s pomočjo določenega znakovnega kodiranja
Charset naborZnakov = StandardCharsets.UTF_8;
String vsebina = new String(bajti, naborZnakov);
```

V kolikor v obstoječem nizu hranimo besedilo, ki ga želimo shraniti v datoteko, to storimo s pomočjo metode `write`:

```java
Path pot = Paths.get("io", "github", "e_gradivo", "besedilo.txt");
String vsebina = "pozdravljen, svet!";
Charset naborZnakov = StandardCharsets.UTF_8;
Files.write(pot, vsebina.getBytes(naborZnakov));

// če želimo zapisati vsebino na konec datoteke, parametrom dodamo še konstanto StandardOpenOption.APPEND
Files.write(pot, vsebina.getBytes(naborZnakov), StandardOpenOption.APPEND);
```

Pri branju in pisanju bajtov smo uporabili razrede `FileInputStream`, `FileOutputStream` in `BufferedReader`, obstaja pa tudi `BufferedWriter`. Namesto neposredne uporabe teh razredov, si lahko pomagamo z metodami razreda `Files`, ki olajšajo ustvarjanje novih objektov:

```java
Path pot = Paths.get("io", "github", "e_gradivo", "besedilo.txt");
Charset naborZnakov = StandardCharsets.UTF_8;

InputStream is = Files.newInputStream(pot);
OutputStream os = Files.newOutputStream(pot);
Reader r = Files.newBufferedReader(pot, naborZnakov);
Writer w = Files.newBufferedWriter(pot, naborZnakov);
```

### Ustvarjanje datotek in map

Kadar želimo zgolj ustvariti datoteko brez vsebine, si pomagamo s statično metodo `createFile` na razredu `Files`. V kolikor datoteka na podani poti že obstaja, se sproži izjema.

```java
Path pot = Paths.get("io", "github", "e_gradivo", "datoteka.txt");
Files.createFile(pot);
```

Ustvarimo lahko tudi eno ali več map. Kadar ustvarjamo samo eno mapo, mora celotna struktura map nad njo že obstajati, v nasprotnem primeru pa je potrebno uporabiti metodo za ustvarjanje več map.

```java
Path potMape = Paths.get("io", "github", "e_gradivo", "podmapa");
Files.createDirectory(potMape);

Path potMap = Paths.get("io", "github", "e_gradivo", "podmapa", "podmapa2", "podmapa3");
Files.createDirectories(potMap);
```

Razred `Files` vključuje dodatne metode za ustvarjanje začasnih datotek in map, glede na podano ali sistemsko določeno lokacijo.

```java
Path potMape = Paths.get("io", "github", "e_gradivo", "podmapa");
String predpona = "pre";
String pripona = "pri";
Path zacDat1 = Files.createTempFile(potMape, predpona, pripona);
Path zacDat2 = Files.createTempFile(predpona, pripona);
Path zacMap1 = Files.createTempDirectory(potMape, predpona);
Path zacMap2 = Files.createTempDirectory(predpona);
```

Podana predpona ali pripona je lahko tudi `null`. V tem primeru se drugi del imena datoteke generira naključno, pri mapah pa se opusti.

### Kopiranje, premikanje in odstranjevanje datotek

Kopiranje datoteke iz ene lokacije na drugo opravimo s pomočjo metode `copy` na razredu `Files`.

```java
Path izPoti = Paths.get("io", "github", "e_gradivo", "datoteka1.txt");
Path naPot = Paths.get("io", "github", "e_gradivo", "datoteka2.txt");
Files.copy(izPoti, naPot);
```

Premikanje datoteke iz prvotne na novo lokacijo opravimo s pomočjo metode `move`.

```java
Path izPoti = Paths.get("io", "github", "e_gradivo", "besedilo.txt");
Path naPot = Paths.get("io", "github", "e_gradivo", "vhodizhod", "besedilo.txt");
Files.move(izPoti, naPot);
```

V primeru, da datoteka, ki jo želimo skopirati ali premakniti na podano pot že obstaja, bo operacija neuspešna. V kolikor bi vseeno radi prepisali obstoječo datoteko na ciljni poti, moramo uporabiti konstanto `StandardCopyOption.REPLACE_EXISTING`. Za kopiranje vseh atributov datoteke uporabimo konstanto `StandardCopyOption.COPY_ATTRIBUTES`.

```java
Path izPoti = Paths.get("io", "github", "e_gradivo", "datoteka1.txt");
Path naPot = Paths.get("io", "github", "e_gradivo", "datoteka2.txt");
Files.copy(izPoti, naPot, StandardCopyOption.REPLACE_EXISTING, StandardCopyOption.COPY_ATTRIBUTES);
```

Odstranjevanje datoteke na navedeni lokaciji opravimo z metodo `delete`. V kolikor datoteka na podani poti ne obstaja, metoda proži izjemo. Kadar nismo prepričani, če bo datoteka obstajala, lahko raje uporabimo metodo `deleteIfExists`.

```java
Path pot = Paths.get("io", "github", "e_gradivo", "vhodizhod", "besedilo.txt");
Files.delete(pot);
boolean odstranjeno = Files.deleteIfExists(pot); // vrne logično vrednost, če je bila datoteka odstranjena ali ne
```

### Informacije datotek

Z razredom `Files` si pomagamo pri pridobivanju različnih informacij o datoteki. Na naslednjem seznamu so metode, ki jim podamo pot ter nato vrnejo logično vrednost:

- `exists` - preverjanje obstoja datoteke
- `isHidden` - preverjanje ali je datoteka skrita
- `isReadable`, `isWritable`, `isExecutable` - preverjanje berljivosti, zapisljivosti in možnost izvajanja datoteke
- `isRegularFile`, `isDirectory`, `isSymbolicLink` - preverjanje ali gre za datoteko, mapo ali simbolično povezavo

Poleg navedenih lahko uporabimo še metodo `size`, ki ji prav tako podamo pot in vrne velikost datoteke v bajtih.

```java
Path pot = Paths.get("io", "github", "e_gradivo", "datoteka.txt");
long velDat = Files.size(pot);
```

### Elementi mape

Datoteke, mape in simbolične povezave na podani poti lahko pridobimo s pomočjo klica metode `list`. Vrača tok _(ang. stream)_, ki nima povezave z vhodnim in izhodnim tokom, temveč z načinom izvajanja operacij in pridobivanja vrednosti v obliki zbirke. V izogib spoznavanju novega koncepta, zato nad njim kličemo metodo `toArray` in ji podamo podatkovni tip tabele, ki jo pričakujemo. Pridobimo seznam poti (absolutno ali relativno) glede na podano pot, ki predstavlja elemente v tej mapi.

```java
Path pot = Paths.get("io", "github", "e_gradivo");
Path[] elementi = Files.list(pot).toArray(Path[]::new);
for (Path element : elementi) {
    System.out.println(element);
}
```

Nad vsako potjo lahko kličemo operacije s pomočjo razreda `Files`, ki smo jih omenili predhodno.
