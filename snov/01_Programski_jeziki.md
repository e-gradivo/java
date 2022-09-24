# Programski jeziki

Programski jezik je stroju berljiv umetni jezik, ki je bil razvit z namenom izražanja operacij za izvajanje na računalniku. Uvrščamo ga med računalniške jezike, uporabljen pa je v namen programiranja računalnikov za implementacijo algoritmov. Njihov zapis je lahko podan v imperativni ali deklarativni obliki.

- Imperativno programiranje se osredotoča na natančno opisovanje načina, kako program deluje korak za korakom. Uporablja različne stavke, ki z izvajanjem spreminjajo stanje v katerem se program nahaja.

- Deklarativno programiranje se osredotoča na opisovanje rezultata, ki ga mora program doseči v okviru reševanja izbrane problemske domene. Pri tem ne definira natančnega načina postopka s katerim je rezultat pridobljen.

## Gradniki

Programski jeziki imajo nekaj osnovnih gradnikov za opis podatkov in procesov/pretvorb, ki se nanašajo nanje. Za primer lahko vzamemo seštevanje dveh števil, pri čemer seštevanje označimo kot proces/pretvorbo, seštevanca pa podatka, nad katerima se ta izvede. Programski jeziki običajno sestojijo iz dveh ključnih komponent - sintakse in semantike, ki opisujeta njihovo strukturo in pomen.

### Sintaksa

Obliki v kateri je definiran programski jezik, rečemo sintaksa. Ta določa združevanje elementov jezika, na primer besed, v višje strukture, na primer stavke. Enolično določa obliko dovoljenih izrazov v danem programskem jeziku. Sintaksa jezika obravnava možne kombinacije znakov in drugih elementov jezika ter njihov medsebojni odnos ne glede na pomen teh kombinacij. Za pomen je odgovorna semantika.

Vsi sintaktično pravilni programi niso nujno pravilni tudi semantično. V primeru slabo napisanih programov, lahko ti ustvarijo napako pri prevajanju ali izvajanju oziroma se obnašajo nepričakovano.

### Semantika

Pomenu jezikovnih elementov pravimo semantika. Posamezni element ima lahko enega ali več pomenov, odvisno od njegove definicije in lokacije, kjer ga uporabljamo. Običajno pravi pomen elementov razberemo šele iz konteksta in načina njihove uporabe.

#### Statična semantika

Statična semantika določa omejitve strukture veljavnih stavkov, ki jih ni mogoče izraziti v okviru sintakse. Za jezike, ki jih prevajamo statična semantika vključuje zlasti tista pravila, ki se jih lahko preveri v času prevajanja. Za primer lahko vzamemo preverjanje, če je vsak gradnik programa dejansko deklariran pred njegovo uporabo.

#### Dinamična semantika

Dinamična semantika določa kdaj in na kakšen način elementi jezika izvedejo določeno obnašanje programa. Za primer lahko semantika definira strategijo, ki določa na kakšen se izrazi izvedejo in spremenijo v vrednosti (pomni seštevanje dveh števil).

### Sistem tipov

Programski jezik določa način opredeljevanja vrednosti in izrazov s pomočjo tipov. Kadar govorimo o tipih posameznih vrednosti, gre za **podatkovne tipe**, kadar govorimo o tipih izrazov, pa gre običajno za **strukturne tipe**. Cilj sistema tipov je preveriti in zagotoviti pravilnost programa glede na operacije, ki jih nadalje izvajamo nad temi vrednostmi ali izrazi.

#### Tipizirani in netipizirani jeziki

Jezik je tipiziran, če specifikacija operacije definira tip podatkov, nad katerim jo lahko izvedemo. V matematiki lahko seštevanje izvedemo nad dvemi števili, ne moremo pa te iste operacije ponoviti nad dvema črkama (operacija za to vrsto podatkov ni definirana). To velja tudi za tipizirane programske jezike, ki preverjajo ustreznost vrednosti podatkov, ki jih navedemo za uporabo v operaciji. Vsaki operaciji zato predhodno določimo tipe podatkov, s katerimi lahko operira.

V nasprotju s tipiziranimi jeziki, obstajajo tudi netipizirani, ki za razliko dovoljujejo izvajanje katerekoli operacije nad podatki kateregakoli tipa. Večina zbirnih jezikov je netipiziranih, podatke pa obravnavajo kot zaporedja bitov različne dolžine, zato tudi rezultat vsake operacije ostane v takšni obliki.

#### Statično in dinamično tipiziranje

Glede na čas prevajanja tipov ločimo dve skupini programskih jezikov:

- statično tipizirane _(ang. statically typed)_
- dinamično tipizirane _(ang. dynamically typed)_

Bistvena razlika med njima je v načinu označevanja podatkov in poznavanja tipov vrednosti.

Pri statično tipiziranih mora programer vedno označiti tip podatka v naprej, zaradi česar morajo tudi vse operacije točno definirati nad katerimi tipi podatkov lahko delujejo.

Pri dinamično tipiziranih se programer ne potrebuje ukvarjati z označevanjem tipa podatkov, saj so ti določeni na osnovi dejanske vrednosti podatka. Še vedno pa morajo biti tipi podatkov za izvedbo končnih operacij med seboj kompatibilni (npr. če program ne definira operacije seštevanja črk in številk, bo še vedno prišlo do napake).

#### Šibko in močno tipizirani jeziki

Glede na način prevajanja tipov programske jezike delimo na:

- šibko tipizirane _(ang. weakly typed)_
- močno tipizirane _(ang. strongly typed)_

Šibko tipizirani jeziki omogočajo, da podatkovni tip ene oblike interpretiramo tudi v drugi, na primer znak s številko '1', kot dejansko številko 1. V določenih primerih je takšen način delovanja zelo uporaben, vendar omogoča pojavljanje napak tako v času prevajanja, kot med izvajanjem programa.

Močno tipizirani jeziki ne odstopajo od navajanja dejanskih podatkovnih tipov za nabor pričakovanih vrednosti. To pomeni, da če moramo v operacijo podati dve številki, za primer vzemimo 3 in 1, morata biti podani kot številki in ne kot številka 3 in znak '1'. V primeru, da to storimo navkljub jasno določenim pravilom, se program ne bo uspešno prevedel.

### Standardna knjižnica in izvajalni sistem

Večina programskih jezikov poleg osnovnih gradnikov zagotavlja še dodaten nabor operacij in orodij v obliki jederne knjižnice _(ang. core library)_ oziroma standardne knjižnice _(ang. standard library)_. Operacije, ki jih najdemo so implementacije najbolj pogostih algoritmov, orodja pa mehanizmi za vnos in izpis podatkov.

Meja med standardno knjižnico in funkcionalnostmi jezika je odvisna od posameznega programskega jezika. V nekaterih primerih je standardna knjižnica popolnoma ločena od programskega jezika, tako kot vsaka zunanja knjižnica, spet v drugih primerih standardna knjižnica definira izbrane gradnike jezika. Slednje velja tudi za Javo. Kadar so gradniki jezika del standardne knjižnice obstaja možnost, da je težko določiti kaj spada vanjo in kaj mora biti del specifikacije jezika.

## Delitev programskih jezikov

Programske jezike kategoriziramo v pet generacij:

1. **Strojni jeziki** _(ang. Machine languages)_: Edina vrsta jezikov, ki jih računalnik lahko obdela neposredno brez predhodne transformacije. Strojna koda _(ang. machine code)_ je tok zaporedja podatkov v dvojiškem (binarnem) številskem sistemu. V pomoč programerju obstajajo gradniki strojnega jezika v desetiški, osmiški ali šestnajstiški obliki, ki jih ta nato sestavi v strojno kodo.
2. **Zbirni jeziki** _(ang. Assembly languages)_: Jeziki, ki zagotavljajo dodaten nivo abstrakcije nad strojno kodo. Človeku poenostavljajo razumevanje logike kode, ki se nato prevede v strojno kodo.
3. **Visoko-nivojski jeziki** _(ang. High-level languages)_: Programski jeziki, ki težijo k bolj strojno neodvisnemu in programersko bolj prijaznemu jeziku, kot strojni in zbirni jeziki. Primeri: C/C++, Java, Python, Go, JavaScript, ...
4. **Domenski jeziki** _(ang. Domain-specific languages)_: Jeziki narejeni s specifično aplikacijo v mislih (npr. podatkovne baze, statistična analiza, ...). Primeri: SQL, MATLAB, LabVIEW, ...
5. **Jeziki pete generacije** _(ang. Fifth-generation languages)_: Programski jeziki osnovani na reševanju težav s pomočjo omejitev, ki jih podamo programu (npr. deklarativni jeziki). Primeri: Prolog, OPS5, Mercury, ...

## Načrtovanje in implementacija

Razvijalci nove programske jezike ustvarijo zaradi potrebe po določenih funkcionalnostih, ki jih v obstoječih jezikih ni, ali pa je njihova uporaba otežena zaradi načina implementacije. Pri oblikovanju posameznega jezika sodelujejo tako oblikovalci, kot tudi uporabniki jezika, saj v procesu ugotovijo ključne prednosti in pomanjkljivosti, ki jih ta ima. V namen nadaljnjega razvoja jezika tako pripravijo številne dokumente, ki pripomorejo pri odločitvah o smeri in prioriteti nadgradenj. Bistvena dokumenta, ki morata biti prisotna za začetek oblikovanja novega jezika sta specifikacija in implementacija.

### Specifikacija

Namen specifikacije programskega jezika je njegov podroben opis, ki ga implementatorji in uporabniki uporabijo pri določanju pravilnosti obnašanja programa glede na izvorno kodo. Glavna pri tem je natančna definicija sintakse, statične semantike, izvajanja semantike jezika.

### Implementacija

Implementacija programskega jezika zagotavlja način pisanja programov v tem jeziku in izvajanja na eni ali več konfiguracij v povezavi s strojno in programsko opremo. V splošnem obstajata dva pristopa k implementaciji programskega jezika:

- prevajanje _(ang. compilation)_
- tolmačenje _(ang. interpretation)_

Pri prevajanju uporabljamo **prevajalnik** _(ang. compiler)_, ki prevede izvorno kodo programa neposredno v strojno kodo ali vmesni program imenovan **tolmač** _(ang. interpreter)_.  V nekaterih implementacijah z uporabo tolmača ni razvidne meje med prevajanjem in tolmačenjem. Programi, ki so izvedeni neposredno na strojni opremi s pomočjo strojne kode so običajno precej hitrejši od tistih, ki uporabljajo tolmačenje.

#### Prevajalnik

Prevajalnik je program, ki prevede kodo iz enega programskega jezika v drugega. Običajno jezik višjega nivoja prevajamo v jezik nižjega nivoja. Pri tem je ciljni jezik ponavadi strojni jezik, vendar obstajajo izjeme, kjer to ne drži. Obstajajo tudi programi, ki prevajajo jezike iz nižjega nivoja v višji, rečemo jim povratni prevajalniki _(ang. decompiler)_.

```text
+------------------+       +------------------+      +------------------+      +------------------+
|                  |       |                  |      |                  |      |                  |
|   Izvorna koda   +------->    Prevajalnik   +------>   Strojna koda   +------>    Izvajanje     |
|                  |       |                  |      |                  |      |                  |
+------------------+       +------------------+      +------------------+      +------------------+
```

#### Tolmač

Tolmač je program, ki direktno izvaja kodo, brez da bi jo najprej prevedel v strojno kodo. To lahko izvaja na več različnih načinov, naprimer s sprotnim prevajanjem ali izvajanjem kode, ki je zapečena v tolmač (je vnaprej prevedena). Pri uporabi sprotnega prevajanja _(ang. just-in-time compilation)_ najprej pridobimo bajtno kodo _(ang. bytecode)_ s pomočjo prevajalnika, nato pa navidezni stroj _(ang. virtual machine)_ ravno pred izvajanjem prevede bloke bajtne kode v strojno kodo za neposredno izvedbo na strojni opremi.

```text
+------------------+       +------------------+      +------------------+
|                  |       |                  |      |                  |
|   Izvorna koda   +------->      Tolmač      +------>    Izvajanje     |
|                  |       |                  |      |                  |
+------------------+       +------------------+      +------------------+
```

## Visoko-nivojski jeziki

V nadaljevanju bomo spoznali osnovne lastnosti nekaterih visoko-nivojskih programskih jezikov, ki so danes med najbolj uporabljenimi. Bistveno pri tem bo razumevanje doslej opisanih konceptov na primerih dejansko obstoječih jezikov. Vsi izmed navedenih so imperativni in splošno namenski programski jeziki.

### Python

Python je dinamično in močno tipiziran programski jezik s poudarkom na berljivosti kode in uporabi točno predpisanih zamikov. Za izvajanje programov napisanih v tem jeziku potrebujemo tolmač.

### JavaScript

JavaScript je dinamično in šibko tipiziran programski jezik, prvotno namenjen izvajanju kode v okviru spletnega brskalnika. Za izvajanje programov napisanih v tem jeziku potrebujemo tolmač. Vsak spletni brskalnik s podporo JavaScriptu vsebuje namenski tolmač, ki omogoča sprotno prevajanje. Poleg spletnih brskalnikov obstajajo tudi druga izvajalna okolja, kjer lahko JavaScript uporabimo za izvajanje operacij izven okolja spleta.

### Go

Go je statično in močno tipiziran programski jezik, ki so ga oblikovali pri Googlu z namenom odpraviti težave, s katerimi so se srečevali pri drugih programskih jezikih. Za izvajanje programov napisanih v tem jeziku uporabljamo prevajalnik, ki iz izvorne kode pripravi strojno kodo za neposredno izvajanje. V zadnjih letih je postal eden izmed najbolj uporabljenih jezikov zaradi poenostavitve izbranih funkcionalnosti, ki so v drugih jezikih težje za implementiranje. Obenem zagotavlja standardno knjižnico, ki vključuje zelo učinkovito implementacijo operacij, ki jih uporabljamo v okviru omrežij in hkratnega procesiranja.

### Java

Java je statično in močno tipiziran programski jezik, ki je nastal z namenom enkratnega razvoja programov in možnosti izvajanja na več različnih končnih platformah. Za izvajanje programov napisanih v tem jeziku uporabljamo tolmač, ki omogoča sprotno prevajanje.

#### Izvajanje programa

Način izvajanja programov v Javi je nekoliko bolj specifičen od prej omenjenih programskih jezikov, saj je razdeljen na dva dela, ki ju mora razumeti tudi programer. Pri sprotnem prevajanju za samo izvajanje najprej potrebujemo bajtno kodo, ki jo moramo pridobiti iz izvorne kode. Za Javo v ta namen obstaja prevajalnik, ki ga uporabimo preden želimo izvesti program. Na osnovi pridobljene bajtne kode, nato lahko to zaženemo v navideznem stroju, ki ga imenujemo **Java Virtual Machine** oziroma **JVM**. Navidezni stroj nato bajtno kodo interpretira in izvede na sistemu.

```text
+------------------+       +------------------+
|                  |       |                  |
|   Izvorna koda   +------->   Prevajalnik    |
|                  |       |                  |
+------------------+       +--------+---------+
                                    |
                                    |
                           +--------v---------+       +------------------+       +------------------+
                           |                  |       |                  |       |                  |
                           |   Vmesna koda    +------->      Tolmač      +------->    Izvajanje     |
                           |   (bytecode)     |       |                  |       |                  |
                           +------------------+       +------------------+       +------------------+
```

Bistveno za tak način delovanja je **popolna prenosljivost**, kar pomeni, da po prevajanju v bajtno kodo, le-to lahko prenesemo na katerokoli platformo s podporo JVM, kjer jo nato izvedemo. Končnemu uporabniku, ki želi uporabljati naš program moramo zato namestiti izvajalno okolje imenovano **Java Runtime Environment** oziroma **JRE**. JRE poleg programskih knjižnic in ostalih datotek zagotavlja implementacijo JVM.

#### Namestitev

Za potrebe razvoja programov v Javi obstaja poseben paket z vsemi orodji, ki jih potrebujemo tekom programiranja. Imenuje se **Java Development Kit** oziroma **JDK**. Glede na namen za katerega želimo razvijati programe, obstajata dve različici:

- [Oracle JDK](https://www.oracle.com/java/technologies/downloads/)
- [OpenJDK](https://adoptopenjdk.net/)

#### Prvi program

Najprej ustvarimo novo datoteko `PozdravljenSvet.java`. Kot razberemo iz imena datoteke, najprej uporabimo poljubno poimenovanje programa, nato pa ime zaključimo s končnico `.java`. Tako vemo, da gre za izvorno kodo v tem programskem jeziku. Datoteko nato odpremo in vanjo zapišemo naslednjo kodo:

```java
class PozdravljenSvet {
    public static void main(String[] args) {
        System.out.println("Pozdravljen, svet!");
    }
}
```

Glede na specifikacijo programskega jezika smo uporabili ustrezne ključne besede, ki po semantični analizi dobijo ustrezen pomen. Podrobneje bomo vse uporabljene gradnike Jave obravnavali tekom nadaljnje snovi. Za končno izvajanje našega programa sledimo prej opisanemu načinu dveh delov, s katerimi lahko naš program uspešno izvedemo.

#### Prevajanje

Sprva moramo naš program prevesti v bajtno kodo, kar storimo s prevajalnikom `javac`, okrajšano za **Java Compiler**. Tako se imenuje tudi program, ki smo ga namestili z JDK, podamo pa mu argument v obliki imena naše datoteke `PozdravljenSvet.java`:

```shell
javac PozdravljenSvet.java
```

Če smo pozorni na vsebino mape v kateri se nahaja prvotna datoteka s končnico `.java`, bomo sedaj opazili, da se je poleg te pojavila še dodatna datoteka s končnico `.class`. Slednja vsebuje bajtno ali vmesno kodo, ki jo nato izvedemo s pomočjo JVM.

#### Izvajanje

Po pridobivanju `.class` datoteke smo izpolnili še zadnjo zahtevo, ki je potrebna pred izvajanjem programa. Uporabimo jo tako, da pokličemo navidezni stroj s pomočjo programa `java` (nameščen z JDK), ki mu podamo argument v obliki imena našega programa `PozdravljenSvet`:

```shell
java PozdravljenSvet
```

Pri klicu programa navedemo zgolj ime programa, kot smo ga zapisali v izvorni kodi. V tem primeru ne pišemo končnice `.class`, saj JVM zna samostojno najti zahtevano datoteko.

#### Interaktivna jezikovna lupina

Z namestitvijo JDK smo pridobili orodje `jshell`, ki nam omogoča hitro preverjanje pravilnosti programskih ukazov. Gre za program namenjen neskončnemu prebiranju in izvajanju ukazov ter izpisu njihovega rezultata ali vrednosti. Tovrstne programe imenujemo REPL _(ang. read-eval-print loop)_. Pripomorejo nam kadar želimo ukaze izvršiti brez predhodnega pisanja kode v datoteko in izvrševanja nadaljnjega postopka, s katerim lahko program izvedemo (v primeru Jave je ta postopek prevajanje v bajtno kodo in izvajanje le-te s pomočjo navideznega stroja).

Program `jshell` deluje kot ukazna vrstica _(ang. command line)_, v katero vnesemo ukaze ali izraze zapisane v programskem jeziku Java. Ob zagonu programa nas pričaka poziv _(ang. prompt)_, ki zahteva vnos.

```text
|  Welcome to JShell -- Version 11.0.16
|  For an introduction type: /help intro

jshell> 
```

Vanj vnesemo želen ukaz/izraz, ki ga želimo izvesti in nato vnos potrdimo (tipka enter). V našem primeru bomo vnesli izraz za seštevanje števil 2 in 3.

```text
jshell> 2 + 3
$1 ==> 5
```

Po potrditvi se izraz prične izvajati, zatem pa pridobimo rezultat (v kolikor ga ukaz/izraz seveda vrača). Kadar je rezultat neka vrednost, se ta samodejno shrani v spremenljivko imenovano z `$` in zaporedno številko vnosa (v našem primeru `$1`). Nanjo se lahko sklicujemo v naslednjih ukazih/izrazih.

```text
jshell> $1 + 5
$2 ==> 10
```

Dodatna funkcionalnost, ki jo lahko uporabimo v okviru `jshell` je pomoč pri zaključevanju ukazov. V primeru, da se sklicujemo na izbran gradnik kode, zatem pritisnemo tipko tab, ki nam vrne možno nadaljevanje našega ukaza.

```text
jshell> System.
Logger                 LoggerFinder           arraycopy(             
class                  clearProperty(         console()              
currentTimeMillis()    err                    exit(                  
gc()                   getLogger(             getProperties()        
getProperty(           getSecurityManager()   getenv(                
identityHashCode(      in                     inheritedChannel()     
lineSeparator()        load(                  loadLibrary(           
mapLibraryName(        nanoTime()             out                    
runFinalization()      setErr(                setIn(                 
setOut(                setProperties(         setProperty(           
setSecurityManager(
```

Zatem preprosto dodamo toliko črk, da se nadaljevanje ukaza ne ujema več z nobenim drugim in ponovno pritisnemo tipko tab za samodejno dokončanje ukaza (za primer vzamemo zapis ukaza `System.o`, nato pritisnemo tab, nakar se ukaz samodejno zaključi kot `System.out`).

```text
jshell> System.out.println("Pozdravljen, svet!")
Pozdravljen, svet!
```

Z uporabo programa `jshell` si torej lahko pomagamo kadarkoli želimo preveriti ali je naš zapis ukaza ali izraza pravilen oziroma ali bo izvedba in rezultat le-tega takšen, kot ga zares pričakujemo.
