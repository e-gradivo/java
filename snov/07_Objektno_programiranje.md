# Objektno programiranje

V tem poglavju spoznamo ključni koncept programiranja, ki je uporabljen v programskem jeziku Java. Osnovne konstrukte objektno usmerjenega programiranja smo pravzaprav uporabljali že v čisto prvem programu, ki smo ga napisali.

Pravi objektno usmerjeni programski jeziki morajo podpirati naslednje lastnosti:

- **Enkapsulacija** _(ang: encapsulation)_: združevanje podatkov in vedenja v celoto, pri čemer implementacijske podrobnosti niso vidne uporabniku.

  Bistveno za pravilno delovanje enkapsulacije je, da nikoli ne dostopamo neposredno do polj drugih razredov, vendar le do lastnih. S tem dosežemo, da se notranja struktura in logika drugega razreda lahko povsem spremeni in to ne vpliva na način uporabe tega razreda v našem. Za način takšnega delovanja obstaja posebno poimenovanje, ki mu pravimo črna škatla _(ang. black box)_.

- **Dedovanje** _(ang: inheritance)_: razširjanje obstoječih razredov z namenom dodajanja nove funkcionalnosti ali spreminjanja obstoječe.

  Nadgradnja obstoječe programske logike lahko vodi v spremembo dosedanjega vedenja. Posledično moramo biti pri razširjanju že napisane kode pozorni na morebitne stranske učinke, ki jih lahko ustvarimo s spremembami.

- **Polimorfizem** _(ang: polymorphism)_: zmožnost deklaracije enotnega vmesnika za več različnih entitet s podobnim vedenjem, pri čemer se rezultat posameznega dejanja na entiteti lahko razlikuje.

  Vedenje v programu lahko določimo vnaprej in tako postavimo okvir v katerem morajo delovati vsi objekti, ki implementirajo določen vmesnik. S tem se izognemo pisanju dodatne kode za obravnavo posameznega objekta in vzpostavimo enotno delovanje, ki med drugim pripomore k boljši berljivosti in lažjemu razumevanju kode.

V nadaljevanju bomo spoznali gradnike, ki omogočajo izpolnjevanje vseh navedenih lastnosti in s tem Javo uvrščajo med prave objektno usmerjene programske jezike.

## Razredi

Razred _(ang. class)_ je predloga ali načrt iz katerega ustvarimo objekte _(ang. objects)_. Predstavljamo si jih lahko kot modele za piškote, objekte pa kot piškote same. S konstruiranjem _(ang. construct)_ objekta iz razreda, naredimo **instanco razreda**.

Vso kodo v Javi pišemo v okviru razredov. Prav tako smo doslej za vse operacije, ki so že na voljo v standardni knjižnici, uporabljali razrede. Teh je na voljo nekaj tisoč in pokrivajo različna področja, kot so uporabniški vmesniki, datumi in koledar ter omrežno programiranje. Kljub temu moramo za reševanje problemov lastne aplikacijske domene še vedno ustvariti razrede, ki zagotavljajo logiko zanje.

Razredi so sestavljeni iz dveh glavnih delov:

- **polje** _(ang. field)_: hrani podatke, ki so definirani z ustreznim podatkovnim tipom.

- **metoda** _(ang. method)_: izvaja operacije nad polji razreda ali podanimi vhodnimi parametri ter lahko vrne rezultat.

```java
class Razred {
    int polje;

    void metoda() {
        // ...
    }
}
```

Dejanska hramba podatkov in izvedba operacij nad njimi je možna šele, ko naredimo instanco razreda oziroma **objekt**. Specifičen objekt ima točno določene vrednosti polj, ki določajo **trenutno stanje** objekta. Z izvedbo metode na objektu to stanje lahko spremenimo.

```java
StringBuffer sb = new StringBuffer("world"); // ustvarimo objekt z začetno vrednostjo
// trenutno stanje/vrednost sb => world
sb.insert(0, "Hello "); // kličemo metodo, s katero vstavimo del niza na začetek in spremenimo stanje objekta
// trenutno stanje/vrednost sb => Hello world
```

Glavne značilnosti objektov:

- **vedenje** _(ang: behavior)_: definira kaj lahko naredimo z objektom (oziroma katere metode lahko uporabimo).

- **stanje** _(ang: state)_: hrani odziv na klic metode.

- **enoznačnost** _(ang: identity)_: omogoča razlikovanje z drugimi, ki imajo isto vedenje in stanje.

Objekti, ki so instance istega razreda se vedno razlikujejo (so enoznačni), saj _običajno_ hranijo drugačno stanje. Značilnosti lahko vplivajo ena na drugo – na primer: Imamo razred `Narocilo` s poljem `status`, ki mu zaporedno določimo vrednost "plačano" in "poslano". Glede na trenutno določen `status` smemo določiti nov status - v kolikor naročilo še ni bilo plačano, ne smemo dovoliti, da se `status` spremeni na vrednost "poslano".

```java
class Narocilo {
    String status = "shranjeno";

    void odposlji() {
        if (status == "plačano") {
            // lahko odpošljemo
        } else {
            // POZOR, naročilo ni bilo plačano, zato ga ne smemo odposlati!
        }
    }
}
```

Pri deklaraciji spremenljivke ali polja, kjer kot podatkovni tip podamo razred, je privzeta vrednost `null`. Označuje, da izbrana spremenljivka ali polje nima dodeljene reference na pomnilniško lokacijo objekta z izbranim podatkovnim tipom.

### Konstruktor

Ustvarjanje nove instance razreda opravimo s pomočjo konstruktorja _(ang. constructor)_. Pomaga nam pri konstruiranju objekta, ki ga želimo uporabiti v nadaljevanju programa. Zapis za ustvarjanje objekta nam je že poznan.

```java
String str = new String("value");
```

Pri tem uporabimo ključno besedo `new`, ki v pomnilniku alocira prostor za objekt in vrne referenco na to pomnilniško lokacijo. V postopku se sproži konstruktor, ki ga definiramo v razredu in je zapisan kot metoda brez podatkovnega tipa, z imenom razreda.

```java
class Narocilo {
    Narocilo() { // konstruktor
        // koda, ki se izvede ob ustvarjanju nove instance razreda
    }
}
```

Objekt za svoje delovanje običajno potrebuje podatke s katerimi ustvari nove podatke, zato konstruktorju lahko podamo tudi parametre. Spomnimo se dveh razredov, ki smo ju že uporabljali na ta način - `String` in `StringBuffer`.

```java
String param = new String(new char[]{ 'p', 'a', 'r', 'a', 'm' }); // podamo tabelo znakov kot parameter konstruktorju
StringBuffer sb = new StringBuffer(5); // podamo kapaciteto kot parameter konstruktorju
```

Parametriziran konstruktor zapišemo tako, da v oklepaju v poljubnem zaporedju navedemo parametre v obliki podatkovnega tipa in imena.

```java
class Narocilo {
    Narocilo(String ime, String priimek, String naslov, int posta, String kraj, String artikli) { // parametriziran konstruktor
        // ...
    }
}
```

Konstruktor se kliče samo ob konstruiranju novega objekta s pomočjo ključne besede `new` in je namenjen nastavljanju začetnega stanja objekta. Posledično ne vrača nobene končne vrednosti.

V kolikor ima kakšen izmed parametrov ne-primitiven podatkovni tip lahko pričakujemo, da bo pri uporabi konstruktorja prišlo do podajanja te vrednosti kot `null`. Običajno želimo dobiti konkreten podatek oziroma objekt, nad katerim lahko izvajamo dodatne operacije oziroma metode. To pomeni, da moramo v konstruktorju preveriti vrednost parametra in potrditi njeno ustreznost.

```java
// primer ustvarjanja objekta, ki mu podano null kot vrednost parametrov z ne-primitivnim podatkovnim tipom
Narocilo nok = new Narocilo(null, null, null, 1000, null, null);

// primer ustvarjanja objekta s pričakovanimi vrednostmi
Narocilo ok = new Narocilo("Ime", "Priimek", "Cesta na naslov 5", 1000, "Ljubljana", "tipkovnica, slušalke, USB ključ");
```

Uporaba metod nad polji, ki imajo nastavljeno vrednost `null` ni mogoča, saj le-te lahko kličemo nad objekti. V kolikor se nam zgodi, da je polje `null` in nad njim kličemo metodo, se v programu pojavi izjema `NullPointerException`, ki nas opozarja na napačen klic.

```java
class Narocilo {
    String imePriimek;

    Narocilo(String ime, String priimek, String naslov, int posta, String kraj, String artikli) {
         // pozor! v kolikor ima parameter ime ali parameter priimek vrednost null, se v okviru spodnje kode sproži NullPointerException
        imePriimek = ime.concat(" ").concat(priimek);
    }
}
```

Obstajata dve rešitvi, ki ju lahko uporabimo v takšnim primerih. Parametrom, ki imajo ne-primitiven podatkovni tip določimo privzeto vrednost ali pa uporabimo metode namenskega razreda `java.util.Objects`, ki prožijo izjeme. Za določanje privzete vrednosti parametra uporabimo pogojni stavek ali metodo `Objects.requireNonNullElse`, za proženje izjeme pa `Objects.requireNonNull`.

```java
class Narocilo {
    String imePriimek;

    Narocilo(String ime, String priimek, String naslov, int posta, String kraj, String artikli) {
        // nastavimo privzeto vrednost s pogojnim stavkom
        ime = (ime == null ? "Ime" : ime);
        priimek = (priimek == null ? "Priimek" : priimek);

        // ali nastavimo privzeto vrednost z metodo Objects.requireNonNullElse
        ime = Objects.requireNonNullElse(ime, "Ime");
        priimek = Objects.requireNonNullElse(ime, "Priimek");

        // ali uporabimo metodo Objects.requireNonNull, ki v primeru null proži izjemo
        ime = Objects.requireNonNull(ime, "Ime je zahtevano!");
        priimek = Objects.requireNonNull(priimek, "Priimek je zahtevan!");

        imePriimek = ime.concat(" ").concat(priimek);
    }
}
```

### Polje

Hranitev podatkov nam omogočajo polja, ki si jih lahko predstavjamo kot globalno spremenljivko razreda. Tako kot spremenljivke je njihov zapis definiran iz podatkovnega tipa in imena.

```java
class Narocilo {
    String status;
    String prevzem = "dostava";

    Narocilo() {
        status = "novo";
    }
}
```

Poljem za uspešno prevajanje razreda ni potrebno določiti vrednosti, vendar dobijo privzeto vrednost podatkovnega tipa (`String => null`, `int => 0`, ...). Pogosto jim vrednost priredimo šele tekom izvajanja logike, zaradi česar moramo biti pozorni, da ne pride do napačne uporabe - v primeru uporabe razreda (kot podatkovni tip) se lahko zgodi, da polje nima dodeljene reference na dejansko pomnilniško lokacijo objekta in tako pride do nepričakovanega dejanja v programu.

Poleg inicializacije polja neposredno ob deklaraciji ali v konstruktorju obstaja dodaten mehanizem imenovan inicializacijski blok. Gre za klasičen blok s kodo, ki ga zapišemo v razred ob ostalih poljih in se izvede ob konstruiranju objekta, pred konstruktorjem.

```java
class Narocilo {
    String status;
    String prevzem = "dostava";
    int dobavaDni;

    // inicializacijski blok
    {
        dobavaDni = 1;
    }

    Narocilo() {
        status = "novo";
    }
}
```

Uporaba tega mehanizma ni pogosta, saj je bolj priročno narediti inicializacijo neposredno ob deklaraciji ali v konstruktorju, v kolikor se navezujemo na vhodne parametre.

### Metoda

Operacije nad podatki razreda, podanimi parametri ali v povezavi s specifično logiko definiramo s pomočjo metod. Lahko vračajo vrednost ali pa se zgolj izvedejo. V osnovi jih zapišemo s podatkovnim tipom in imenom, v oklepajih pa po potrebi sledijo vhodni parametri.

```java
class Narocilo {
    int id;
    String status;

    String oznaka() { // metoda, ki vrača rezultat podatkovnega tipa String
        return "ORDR" + id;
    }

    void shrani() { // metoda, ki ne vrača rezultata
        // ...
    }
}
```

Metode, ki vračajo vrednost morajo imeti podan specifičen podatkoven tip, v katerem bo vrnjena končna vrednost. Za vračanje moramo uporabiti ključno besedo `return`, za njo pa zapišemo dejansko vrednost ali spremenljivko ali polje, ki je rezultat klica metode. Pri tovrstnih metodah je vračanje podatka obvezno, saj sicer ne moremo prevesti kode.

Pri metodah, ki se le izvedejo namesto podatkovnega tipa uporabimo ključno besedo `void`. Označuje, da metoda ne vrne podatka. V tovrstnih metodah ne moremo vračati vrednosti oziroma uporaba ključne besede `return` v njih ni dovoljena.

Sprejem dodatnih podatkov v metodo opravimo s pomočjo parametrov. Definiramo jih v poljubnem zaporedju, njihov zapis pa sestoji iz podatkovnega tipa in imena.

```java
class Narocilo {
    // ...

    void nastaviOpombo(String besedilo) { // pričakujemo parameter besedilo
        // ...
    }

    int pridobiDostavniCas(boolean vipStranka, String vrstaPostnine) { // pričakujemo parametra vipStranka in vrstaPostnine
        if (vipStranka && vrstaPostnine.equals("hitra")) {
            return 1;
        }
        // ...
        return 3;
    }
}
```

Z vidika uporabe poznamo dve vrsti metod:

- s spremembo _(ang. mutator method)_
- z dostopom _(ang. accessor method)_

Obe vrsti smo že uporabljali na objektih, ki smo jih ustvarili s pomočjo razredov za delo z nizi. Metode s spremembo smo uporabljali pri objektih razreda `StringBuffer`, z dostopom pa pri objektih razreda `String`.

```java
StringBuffer sb = new StringBuffer();
sb.append("hello"); // prožimo metodo s spremembo (ang. mutator method)

String s = "world";
s.charAt(2); // prožimo metodo z dostopom (ang. accessor method)
```

Pri metodah s spremembo je bistveno, da z njihovim klicem spremenimo notranje stanje objekta, kar povzroči tudi spremembo njihovega vedenja ali končnih vrednosti metod. S tem vplivamo na prihodnje ukaze v programu, zato se moramo zavedati kaj je posledica izvedbe teh metod.

Pri metodah z dostopom je ravno obratno, saj z njihovim klicem le dostopamo do specifične vrednosti objekta in pri tem ne spremenimo notranjega stanja. Če želimo posodobiti stanje objekta brez, da se to ohrani na obstoječem, naredimo kombinirano metodo, ki vrne nov objekt z želenim stanjem.

### Poimenovanje

Smiselno je, da razrede poimenujemo po glavnem delu logike za katerega so namenjeni. V primeru, ki je uporabljen v delčkih kode, gre za naročilo, ki združuje funkcionalnost še vseh ostalih razredov (npr. `Stranka`, `Naslov`, `Artikel`, ...), ki pri običajnem naročilu tvorijo celoto. Posledično smo ta razred poimenovali `Narocilo` - načeloma lahko v imenih uporabljamo tudi šumnike, vendar upoštevamo najboljše prakse in se temu skušamo izogibati. Na podlagi imena razreda poimenujemo še datoteko, kamor pišemo kodo tega razreda, in sicer z `Narocilo.java`. Na tem mestu zaenkrat samo omenimo, da je ustvarjanje več lokalnih razredov _(ang. local class)_ v isti datoteki dovoljeno, medtem ko mora javni razred _(ang. public class)_ ustrezati imenu datoteke (npr. `Narocilo => Narocilo.java`, `Stranka => Stranka.java`, `Naslov => Naslov.java`, `Artikel => Artikel.java`, ...). Več o dostopnosti (lokalni, javni, ...) razredov pa v nadaljevanju.

### Prepoznavanje in relacije

Pri proceduralnem programiranju začnemo s postopkom programa na vrhu, v okviru funkcije `main`. Objektno usmerjeni način programiranja nima določenega začetka ali točnega postopka, po katerem se ravnamo pri oblikovanju programa. To pomeni, da moramo sami prepoznati razrede - entitete ter njihove metode in uokviriti logiko delovanja, ki jo želimo obravnavati v programu.

Enostavno pravilo po katerem se lahko ravnamo pri prepoznavanju gradnikov programa je, da pri opisu problema, ki ga rešujemo s programom, preverimo samostalnike in glagole. Samostalniki so enakovredni razredom, glagoli pa metodam, ki jih razredi opravljajo.

Vzemimo primer sistema za obdelavo naročil in preglejmo nekaj samostalnikov, ki jih srečamo v procesu:

- Artikel
- Naročilo
- Naslov
- Plačilo
- Stranka

Za vse naštete lahko ustvarimo nove razrede in jim pripišemo določen del funkcionalnosti v programu. S tem razbijemo problem na več logičnih delov in opravljanje posamezne naloge prepustimo tistemu, ki je za to zadolžen ali najbolj ustrezen.

Metode za primer naročila najdemo s pomočjo glagolov. Aritkle *dodamo* naročilu. Naročilo smo *odposlali* ali *preklicali*. Z vsakim glagolom, kot je "dodati", "odposlati", "preklicati", "uveljaviti", identificiramo objekt, ki nosi odgovornost za opravljanje določene naloge. Vsi našteti glagoli ustrezajo razredu `Naročilo`, saj ta hrani vse podatke, s katerimi lahko opravimo posamezno dejanje. Na objektu razreda `Naročilo` bi tako lahko z metodo `dodaj` vključili dodatne objekte razreda `Artikel`.

```java
class Narocilo {
    Artikel[] artikli;

    void dodaj(Artikel artikel) {
        artikli[0] = artikel;
    }
}
```

Objekte razredov, ki tvorijo logično celoto med seboj povezujemo. Najbolj pogoste relacije med razredi so:

- **Odvisnost** _(ang. dependence)_: Relacija "uporablja" pomeni, da razred `A` v okviru svojega delovanja uporablja funkcionalnost/metode razreda `B`.
- **Združevanje** _(ang. aggregation)_: Relacija "ima" pomeni, da razred `A` vključuje objekte razreda `B`.
- **Dedovanje** _(ang. inheritance)_: Relacija "je" pomeni, da razred `NovA` razširja funkcionalnost obstoječega razreda `A`.

### Preobložitev _(ang. overloading)_

Razred ali metoda na osnovi podanih parametrov lahko spremenita vedenje oziroma končni rezultat. Iz tega razloga v Javi obstaja možnost preobložitve konstruktorja in metode. Pomen tega izraza je zgolj v tem, da smemo v kodi konstruktor/metodo napisati večkrat, pri čemer mora imeti podane različne parametre (v nasprotnem primeru nas na napako opozori prevajalnik). Na osnovi različnih parametrov lahko prilagodimo logiko delovanja razreda ali metode in tako obravnavamo dodatne primere, ki se pojavijo med razvojem programa.

```java
class Narocilo {
    int id;
    String status;

    Narocilo() { // konstruktor brez parametrov
        id = 1;
        status = "novo";
    }

    Narocilo(int idParam) { // preobložen konstruktor s parametrom
        id = idParam;
        status = "novo";
    }

    Narocilo(int idParam, String statusParam) { // preobložen konstruktor z dvema parametroma
        id = idParam;
        status = statusParam;
    }
}
```

Poimenovanje, ki ga uporabljamo za dodatne konstruktorje in metode je:

- preobloženi konstruktor _(ang. overloaded constructor)_
- preobložena metoda _(ang. overloaded method)_

```java
class Narocilo {
    String opomba;
    int opombaPomembnost;
    String opombaTip;

    void nastaviOpombo(String besedilo) { // metoda z enim parametrom
        opomba = besedilo;
    }

    void nastaviOpombo(String besedilo, int pomembnost) { // preobložena metoda z dvema parametroma
        opomba = besedilo;
        opombaPomembnost = pomembnost;
    }

    void nastaviOpombo(String besedilo, int pomembnost, String tip) { // preobložena metoda s tremi parametri
        opomba = besedilo;
        opombaPomembnost = pomembnost;
        opombaTip = tip;
    }
}
```

### Implicitni in eksplicitni parametri

Metode operirajo na objektih in dostopajo do polj njihovih instanc. Za primer vzemimo spodnjo metodo `upostevajPopust`.

```java
class Narocilo {
    double cenaSkupaj;
    double popustOdstotek;

    void upostevajPopust(double odstotek) {
        double popust = cenaSkupaj * odstotek / 100;
        cenaSkupaj -= popust;
        popustOdstotek = odstotek;
    }
}
```

Ta nastavi novo vrednost polju `cenaSkupaj` na objektu, kjer kličemo to metodo.

```java
Narocilo narocilo1 = new Narocilo(...); // ustvarimo novo naročilo
// izvedemo ostalo programsko logiko v povezavi z naročilom
narocilo1.upostevajPopust(10); // klic metode
```

Sedaj prevedemo kodo in parametre metode `upostevajPopust` v psevdokodo, ki ponazarja kaj točno kličemo oziroma kakšne operacije izvedemo.

```text
double popust = narocilo1.cenaSkupaj * 10 / 100;
narocilo1.cenaSkupaj -= popust;
narocilo1.popustOdstotek = odstotek;
```

Opazimo, da ima metoda `upostevajPopust` v bistvu dva parametra. Prvi je *implicitni* parameter in sicer objekt razreda `Narocilo`. Drugi parameter, ki ga podamo v oklepajih za imenom metode pa je *eksplicitni* parameter. Kot lahko vidimo je eksplicitni parameter izrecno zapisan pri deklaraciji metode, medtem ko implicitni parameter ni neposredno naveden.

Razlog za izogibanje navedbi implicitnega parametra je v kontekstu, saj kodo pišemo v razred, ki mu pripada zapisana logika. Kljub temu se lahko pojavijo situacije, ko moramo biti bolj specifični in navesti implicitni parameter. Zanj obstaja posebna ključna beseda `this`, ki se sklicuje na trenutni kontekst razreda oziroma njegovo instanco. Metodo `upostevajPopust` lahko popravimo in zapišemo še z implicitnim parametrom.

```java
void upostevajPopust(double odstotek) {
    double popust = this.cenaSkupaj * odstotek / 100;
    this.cenaSkupaj -= popust;
    this.popustOdstotek = odstotek;
}
```

Navedba implicitnega parametra nam pride prav, na primer ko imamo v metodi ali konstruktorju parametre z istim imenom, kot polja razreda.

```java
class Narocilo {
    String naslov;

    Narocilo(String naslov) {
        this.naslov = naslov; // uporabimo implicitni parameter za dostop do polja z istim imenom, kot ga ima ime parametra
    }
}
```

Z implicitnim parametrom si pomagamo še, kadar imamo v razredu definiranih več (preobloženih) konstruktorjev in se v enem želimo sklicevati na drugega. Klic obstoječega konstruktorja mora biti podan kot prvi ukaz v trenutnem konstruktorju.

```java
class Narocilo {
    int id;
    String naslov;
    String dostava;
    int dostavaDni;

    Narocilo(String naslov) {
        this.naslov = naslov;
    }

    Narocilo(String naslov, String dostava) {
        this(naslov); // kličemo predhodni konstruktor
        this.dostava = dostava;
    }

    Narocilo(String naslov, String dostava, int dostavaDni) {
        this(naslov, dostava); // kličemo predhodni konstruktor
        this.dostavaDni = dostavaDni;
    }

    Narocilo(int id, String naslov) {
        this(naslov, "pošta", 1); // kličemo predhodni konstruktor s privzetimi podatki
        this.id = id;
    }
}
```

### Dostopnost

Razredi vključujejo dodaten koncept dostopnosti, ki je namenjen omejevanju klicev in pridobivanju vrednosti v posameznih objektih izven specifičnega nivoja. Dostopnost je ključnega pomena za omogočanje enkapsulacije, saj z njo določimo pod kakšnimi pogoji dostopamo do izbranega programskega gradnika. Java pozna dva nivoja dostopov - vrhnjega _(ang. top level)_ in članskega _(ang. member level)_. Vrhnji nivo je določen s paketi _(ang. package)_, članski pa z razredi.

Obstajajo tri stopnje dostopa:

- javni _(ang. public)_
- zaščiteni _(ang. protected)_
- zasebni _(ang. private)_

Vsak izmed njih določa iz kje lahko oziroma ne smemo dostopati do posameznega programskega konstrukta. Nivoja dostopov v javi imata določene tudi stopnje:

- vrhnji nivo - javni ali paketno-zasebni _(ang. package-private)_ dostop
- članski nivo - javni, zaščiteni in zasebni ter paketno-zasebni

V primeru vrhnjega nivoja ali paketa to pomeni, da kadar znotraj njega navedemo javne člane ali razrede, lahko do njih dostopamo iz vseh ostalih paketov. Paketno-zasebni dostop nima svoje posebne stopnje dostopa, vendar pomeni le, da v kolikor ne podamo specifičnega dostopa (za pakete je možen samo javni), je ta gradnik omejen na paket v katerem se nahaja.

V primeru članskega nivoja ali razreda (velja tudi za druge programske konstrukte in njihove lastnosti, ki jih doslej še nismo omenili in spadajo med člane) to pomeni, da kadar znotraj njega navedemo javna polja ali metode ali konstruktorje, lahko do njih dostopamo iz vseh ostalih paketov in razredov. Do zaščitenih polj/metod/konstruktorjev lahko dostopamo samo iz trenutnega paketa. Do zasebnih polj/metod/konstruktorjev lahko dostopamo samo iz trenutnega člana oziroma razreda.

Dostop posameznemu programskemu gradniku omejimo s pomočjo ključnih besed `public`, `protected` in `private`. Napišemo jih pred definicijo razreda (oz. drugega članskega konstrukta), polja, metode ali konstruktorja.

```java
public class Narocilo {
    private String naslov;
    private String dostava;

    private Narocilo(String naslov) {
        this.naslov = naslov;
    }

    public Narocilo(String naslov, String dostava) {
        this(naslov);
        this.dostava = dostava;
    }

    public String vrniNaslov() {
        return naslov;
    }

    protected String vrniDostavo() {
        return dostava;
    }
}
```

V kolikor želimo iz določenega dela kode dostopati do drugega, ki je omejen in praviloma do njega nimamo dostopa, se program ne prevede in nam vrne napako.

```java
Narocilo ok = new Narocilo("naslov", "pošta"); // kliče se javni konstruktor - koda je pravilna
Narocilo nok = new Narocilo("naslov"); // program se ne prevede, saj je konstruktor s tem parametrom zaseben
```

Primer dostopa, ki je dovoljen na posameznem nivoju si lahko predstavljamo s pomočjo dveh objektov istega razreda. Na ogled vzemimo zgoraj definiran razred `Narocilo` in zasebno polje z nizom `naslov`. Kot vemo je dostop do zasebnega polja iz metod dovoljen, malo manj običajno pa se zdi, da ko prejmemo kot argument objekt istega razreda, še vedno lahko dostopamo do njegovega zasebnega polja.

```java
public class Narocilo {
    private String naslov;

    public Narocilo(String naslov) {
        this.naslov = naslov;
    }

    public boolean istiNaslov(Narocilo narocilo) {
        return narocilo.naslov.equals(naslov); // dostop do zasebnega polja objekta istega razreda je dovoljen
    }
}
```

V glavnem delu programa izvedemo primerjavo in dobimo pričakovan rezultat.

```java
Narocilo nar1 = new Narocilo("naslov");
Narocilo nar2 = new Narocilo("naslov");
System.out.println(nar1.istiNaslov(nar2)); // izpiše se logična vrednost true, saj sta naslova obeh objektov enaka
```

### Pridobivalci in nastavljalci

Java ima za zaščito internih podatkov razreda poseben koncept, ki mu pravimo pridobivalci in nastavljalci _(ang. getters and setters)_. Namenjen je dopolnjevanju koncepta dostopnosti in omogoča enkapsulacijo v pravem pomenu. Bistveno pri tem je, da so polja razreda zasebna, njihovo vrednost pa dobimo s pomočjo **pridobivalca** _(ang. getter)_ ter jo smemo spreminjati zgolj s pomočjo **nastavljalca** _(ang. setter)_.

Pridobivalec je metoda, ki ima isti podatkovni tip, kot polje katerega vrednost vračamo ter vrača vrednost polja. Po konvenciji imajo vse tovrstne metode predpono `get`. Za primer, če bi želeli dobiti vrednost polja `address` s podatkovnim tipom `String`, bi tako napisali metodo `String getAddress()`.

Nastavljalec je metoda tipa `void`, ki sprejme parameter podatkovnega tipa, ki ustreza polju ter temu polju tudi nastavimo vrednost parametra. Po konvenciji imajo vse tovrstne metode predpono `set`. Za primer, če bi želeli nastaviti vrednost polju `address` s podatkovnim tipom `String`, bi tako napisali metodo `void setAddress(String address)`.

```java
public class Narocilo {
    private String naslov;

    public String getNaslov() {
        return naslov;
    }

    public void setNaslov(String naslov) {
        this.naslov = naslov;
    }
}
```

Razlog, da ne dostopamo do polj objektov neposredno je v morebitni logiki, ki jo ima pridobivanje ali nastavljanje. V kolikor ta obstaja, bi neposreden dostop/spreminjanje lahko vplivalo na stanje objekta in s tem privedlo do nepričakovanih situacij, ki jih logika razreda ne zajema. V pridobivalce in nastavljalce torej pišemo tudi kodo, ki zajema vso logiko za ustrezno spremembo stanja razreda, v kolikor je ta zahtevana. Nastavljalci lahko opravljajo tudi preverjanje vrednosti parametra in to vrednost nastavijo na polje le pod določenim pogojem ali v primeru nepravilnih vrednost sprožijo izjemo.

```java
public class Narocilo {
    private String naslov;

    public String getNaslov() {
        return naslov;
    }

    public void setNaslov(String naslov) {
        Objects.requireNonNull(naslov, "Naslov mora biti dejanski niz!");
        if (naslov.toLowerCase().startsWith("cesta")) {
            this.naslov = naslov;
        }
    }
}
```
