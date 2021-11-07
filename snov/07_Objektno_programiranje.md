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

### Polje

Hranitev podatkov nam omogočajo polja, ki si jih lahko predstavjamo kot globalno spremenljivko razreda. Tako kot spremenljivke je njihov zapis definiran iz podatkovnega tipa in imena.

```java
class Narocilo {
    String status;

    Narocilo() {
        status = "novo";
    }
}
```

Poljem za uspešno prevajanje razreda ni potrebno določiti vrednosti, vendar dobijo privzeto vrednost podatkovnega tipa (`String => null`, `int => 0`, ...). Pogosto jim vrednost priredimo šele tekom izvajanja logike, zaradi česar moramo biti pozorni, da ne pride do napačne uporabe - v primeru uporabe razreda (kot podatkovni tip) se lahko zgodi, da polje nima dodeljene reference na dejansko pomnilniško lokacijo objekta in tako pride do nepričakovanega dejanja v programu.

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
