# Dedovanje

V tem poglavju se osredotočimo na enega izmed ključnih konceptov objektno usmerjenega programiranja, ki smo ga prej nekajkrat že omenili in skušali na kratko predstaviti njegovo vlogo.

Dedovanje omogoča, da uporabimo (ali podedujemo) polja in metode obstoječega razreda, pri čemer lahko dopolnimo njihovo logiko v okviru novega razreda.

## Nadrazredi in podrazredi

Uporabo koncepta dedovanja bomo prikazali na primeru izračuna plač v organizaciji z dvemi vlogami - zaposlenimi in managerji. Bistvena razlika med vlogama je le v podrobnostih, saj so managerji prav tako zaposleni, le da imajo nekoliko drugačen nabor nalog, ki jih morajo opraviti. Ena izmed podrobnosti je v načinu izračuna plače. Od zaposlenih pričakujemo, da bodo opravili njim določene naloge in zato prejeli v naprej dogovorjeno plačilo. To drži tudi za managerje, vendar poleg osnovnega plačila dobijo tudi bonus za uspešnost pri doseganju ciljev določenih s poslovnim načrtom podjetja. Iz opisa razberemo, da bomo potrebovali dva razreda, ki ju poimenujemo `Zaposleni` in `Manager`. Obema lahko zapišemo isto osnovno logiko izplačevanja, v razredu `Manager` pa vključimo še bonus. Upoštevamo definicijo dedovanja, ki pravi, da polja in metode obstoječega razreda razširimo z novim razredom. To pomeni, da v razred `Zaposleni` zapišemo osnovno logiko izplačevanja, v razredu `Manager` pa to dopolnimo z njemu lastno logiko dodeljevanja bonusov. Med razredoma `Zaposleni` in `Manager` tako nastane relacija "je" _(ang. is-a)_, saj vsak `Manager` **je** `Zaposleni`.

```java
package io.github.e_gradivo.dedovanje;

public class Zaposleni {
    private String imePriimek;
    private double placa;

    public Zaposleni(String imePriimek, double placa) {
        this.imePriimek = imePriimek;
        this.placa = placa;
    }

    public String getImePriimek() {
        return imePriimek;
    }

    public double getPlaca() {
        return placa;
    }
}
```

Najprej ustvarimo razred `Zaposleni`, kjer navedemo zahtevane podatke, da lahko identificiramo posamezno osebo in pridobimo višino njene plače. Preden ustvarimo še razred `Manager` pa moramo spoznati način, kako dedujemo iz obstoječega razreda `Zaposleni`.

### Ustvarjanje podrazredov

Obstoječe razrede uporabimo oziroma razširimo s pomočjo ključne besede `extends`, ki jo zapišemo ob navedbi razreda in njegovega imena. Poleg ključne besede moramo zapisati tudi ime razreda, ki ga razširjamo. Pri tem se lahko navežemo na relacijo, ki je za dotični primer - vsak `Manager` **je** `Zaposleni`, ko pa to pretvorimo v kodo, je zapis `Manager` **extends** `Zaposleni`.

```java
package io.github.e_gradivo.dedovanje;

public class Manager extends Zaposleni {
    // ...
}
```

Ključna beseda `extends` označuje, da ustvarjamo razred, ki prevzame vse definirane programske konstrukte obstoječega razreda, ki ga navajamo. Obstoječemu razredu rečemo **nadrazred** _(ang. superclass)_, osnovni razred _(ang. base class)_, glavni razred _(ang. core class)_ ali starševski razred _(ang. parent class)_. Novemu razredu, ki razširja obstoječega pa **podrazred** _(ang. subclass)_ ali otrok _(ang. child class)_. Izraza **nadrazred** in **podrazred** sta med javanskimi programerji največkrat uporabljena. Pogosto se v okviru dedovanja uporablja tudi analogijo starš/otrok, ki sovpada s konceptom dednosti v realnem svetu.

Kot zanimivost omenimo, da pri največkrat uporabljenih izrazih predponi _nad_ in _pod_ izhajata iz (diskretne) matematike in se navezujeta na množice _(ang. sets)_. Množica vseh zaposlenih vsebuje množico managerjev oziroma je nadmnožica množice managerjev. Obratno lahko zapišemo tudi, da je množica managerjev podmnožica množice vseh zaposlenih.

Razred `Zaposleni` je nadrazred, pri čemer pomen te besede označuje samo hierarhično pozicijo v relaciji "je". Podrazred (`Manager`) razširja oziroma "je" nadrazred (`Zaposleni`). Običajno nadrazredi vključujejo manj funkcionalnosti, kot podrazredi, ki jih razširjajo. V nadaljevanju primera bomo na podrazredu `Manager` dodali zaenkrat še manjkajoče funkcionalnosti in s tem prikazali, da bo na koncu ta razred enkapsuliral več logike, kot njegov starševski razred `Zaposleni`.

### Konstruktorji podrazreda

Razširjanje nadrazreda zahteva upoštevanje njegovih konstruktorjev v podrazredu. To pomeni, da kadar nadrazred ne vključuje praznega konstruktorja, moramo v podrazredu nujno ustvariti nov konstruktor, preko katerega bomo lahko klicali konstruktor v nadrazredu. Podobno, kot pri inicializaciji novega objekta - če prazen konstruktor ne obstaja, moramo objekt konstruirati preko ustreznega konstruktorja z določenimi parametri.

Ob prevajanju doslej napisane kode razreda `Manager` naletimo na napako, ki pravi, da podan (prazen) konstruktor ne ustreza nobenemu konstruktorju nadrazreda `Zaposleni`. Posledično moramo ustvariti konstruktor, ki bo ustrezal konstruktorju nadrazreda.

```java
package io.github.e_gradivo.dedovanje;

public class Manager extends Zaposleni {
    public Manager(String imePriimek, double placa) {
        // ...
    }
}
```

Po zapisu definicije konstruktorja z dvemi parametri, ki ustrezata konstruktorju nadrazreda lahko poskusimo znova prevesti kodo, vendar kljub temu naletimo na isto napako. Razlog je v tem, da moramo v konstruktorju razreda `Manager` prevajalnik usmeriti na konstruktor nadrazreda, na katerega se želimo sklicevati. Uporabimo ukaz `super()` in mu podamo parametre glede na obstoječ konstruktor nadrazreda.

```java
package io.github.e_gradivo.dedovanje;

public class Manager extends Zaposleni {
    public Manager(String imePriimek, double placa) {
        super(imePriimek, placa);
    }
}
```

Konstruktor podrazreda in število parametrov, ki jih sprejme, se lahko razlikuje od konstruktorjev nadrazreda. Glavno je, da v bloku konstruktorja zapišemo ukaz `super()` in podamo ustrezne parametre. Zapis ukaza mora biti po pravilih prvi v bloku, v nasprotnem primeru se razred ne prevede.

Konstruktor nadrazreda moramo uporabiti iz razloga nastavljanja vrednosti njegovim poljem, saj imajo zasebno stopnjo dostopnosti in jih posledično nastavimo ob inicializaciji, tako kot pri konstruiranju novega objekta.

Pri uporabi ukaza `super()` v konstruktorju, se lahko navežemo na uporabo ključne besede `this`. V konstruktorju smo jo uporabili kadar smo se želeli navezovati na obstoječ konstruktor z drugačnimi parametri. Tudi tam je bil pogoj, da je ukaz s klicem drugega konstruktorja na prvem mestu v bloku konstruktorja.

### Dopolnjevanje podrazreda

V podrazredu zapišemo vso dodatno logiko, ki je specifična zanj in razširja nadrazred.

```java
package io.github.e_gradivo.dedovanje;

public class Manager extends Zaposleni {
    private double bonus;

    // ...

    public void setBonus(double bonus) {
        this.bonus = bonus;
    }
}
```

Z dopolnitvijo razreda `Manager` smo vsem objektom tega razreda dodali možnost nastavljanja decimalne vrednosti bonusa. To pomeni, da ti objekti lahko uporabljajo metodo `setBonus`, medtem pa se nadrazred `Zaposleni` nikakor ne spremeni. Funkcionalnost podrazreda ne vpliva na nadrazred, velja le, da podrazred "je" nadrazred, saj vključuje tudi njegovo funkcionalnost.

```java
Zaposleni zaposleni = new Zaposleni("Ime Priimek", 897.65);
zaposleni.getImePriimek(); // klic je veljaven
zaposleni.getPlaca(); // klic je veljaven
zaposleni.setBonus(123.45); // pozor, metoda setBonus na razredu Zaposleni ne obstaja in ta klic ni veljaven!

Manager manager = new Manager("Im Pri", 1234.567);
manager.getImePriimek(); // klic je veljaven
manager.getPlaca(); // klic je veljaven
manager.setBonus(987.65); // razred Manager vsebuje metodo setBonus, zato je ta klic veljaven
```

Povzetek polj in metod za razred `Zaposleni`:

- `private String imePriimek`
- `private double placa`
- `public String getImePriimek()`
- `public double getPlaca()`

Povzetek polj in metod za razred `Manager`:

- `private String imePriimek` (dedovano iz nadrazreda `Zaposleni`)
- `private double placa` (dedovano iz nadrazreda `Zaposleni`)
- `private double bonus`
- `public String getImePriimek()` (dedovano iz nadrazreda `Zaposleni`)
- `public double getPlaca()` (dedovano iz nadrazreda `Zaposleni`)
- `public void setBonus(double bonus)`

V podrazredu torej na nek način označujemo samo spremembe od nadrazreda, ki ga razširjamo. Upoštevati moramo, da je v nadrazred vključena le splošna logika, ki je skupna vsem nadaljnjim podrazredom. Specifične funkcionalnosti, ki so namenjene le točno določenemu delu našega programa torej uvrstimo v podrazred. S tem omogočimo vzpostavitev hierarhije za logične dele programa in se v primeru kasnejših potreb po dopolnitvi programske logike navežemo na tistega, ki ji najbolj ustreza. V naprej pa mnogokrat ne moremo predvideti možnih razširitev programa, zato je v okviru objektnega programiranja ustaljena praksa izločanja skupne kode v lastni razred in prestrukturiranja logike. To opravimo, ko je problem programa natančneje definiran in s tem kodo oblikujemo v bolj smiselno celoto. Pri tem eno ključnih vlog igra prav koncept dedovanja.

### Prepisovanje metod

Kadar želimo spremeniti logiko določene metode v podrazredu, jo moramo prepisati. V primeru razreda `Manager` je takšna metoda `getPlaca`, saj po razširjanju nadrazreda vključuje le osnovno logiko vračanja plače, brez upoštevanja bonusa. Prepisovanje metode opravimo tako, da njeno definicijo v celoti prepišemo, kot je v nadrazredu, nato pa v blok zapišemo podrazredu lastno logiko.

```java
package io.github.e_gradivo.dedovanje;

public class Manager extends Zaposleni {
    // ...

    public double getPlaca() {
        // ...
    }
}
```

Način izračuna plače za managerja je preprost, saj samo seštejemo osnovno plačo z bonusom. Poskusimo implementirati to v metodo `getPlaca`.

```java
package io.github.e_gradivo.dedovanje;

public class Manager extends Zaposleni {
    // ...

    public double getPlaca() {
        return placa + bonus; // ni veljavno
    }
}
```

Pri prevajanju napisane kode, nam prevajalnik sporoči, da do polja `placa`, ki smo ga definirali v nadrazredu `Zaposleni` ne moremo dostopati, saj ima stopnjo dostopnosti `private`. To pomeni, da do polja lahko dostopamo samo znotraj razreda v katerem smo ga navedli, ne pa tudi v ostalih. Možna rešitev bi bila sprememba stopnje dostopnosti v `protected` oz. privzeto paketno-zasebno stopnjo, vendar s tem omogočimo dostop do polja vsem ostalim razredom v paketu. Iz vidika enkapsulacije to ni najboljša rešitev, zato raje poskusimo uporabiti obstoječo metodo in jo združiti s prepisano.

```java
package io.github.e_gradivo.dedovanje;

public class Manager extends Zaposleni {
    // ...

    public double getPlaca() {
        double osnovnaPlaca = getPlaca(); // katero metodo kličemo tukaj - iz nadrazreda ali trenutno?
        return osnovnaPlaca + bonus;
    }
}
```

V napisani kodi se sedaj sklicujemo na metodo `getPlaca`, vendar pri izvajanju naletimo na izjemo. Težava je namreč v tem, da se sklicujemo na trenutno prepisano metodo, kar povzroči neskončno gnezdeno klicanje te metode in privede do izjeme. Rezultata s takšno kodo ne moremo pridobiti, saj se klici metod nikoli ne prenehajo - mehanizem v Javi na določeni točki prepreči nadaljnje izvajanje in zato pride do izjeme.

Vemo, da bi klic na starševsko metodo (`getPlaca` v razredu `Zaposleni`) rešil težavo, saj vrača le vrednost iz polja `placa` in ne vsebuje drugih klicev, ki bi lahko povzročili problem, kot ga je prepisana metoda. V ta namen uporabimo ključno besedo `super`, ki znotraj podrazreda omogoča dostop do programskih konstruktov dosegljivih v nadrazredu.

```java
package io.github.e_gradivo.dedovanje;

public class Manager extends Zaposleni {
    // ...

    public double getPlaca() {
        double osnovnaPlaca = super.getPlaca(); // kličemo metodo iz nadrazreda
        return osnovnaPlaca + bonus;
    }
}
```

S tem popravkom je koda postala delujoča in logično pravilna. Na podoben problem smo naleteli v poglavju objektnega programiranja, ko smo se želeli sklicevati na polje razreda, v primeru ko ima parameter metode enako ime. Kot rešitev smo spoznali implicitni parameter `this`. Izpostaviti moramo pomembno razliko, saj `super` v primerjavi z `this` ne predstavlja reference na objekt, temveč omogoča usmeritev prevajalnika na programski konstrukt iz nadrazreda.

V podrazredu `Manager` smo napisali prepisano metodo, s katero spremenimo njeno delovanje za ta podrazred. Dodamo torej lahko dodatna polja in metode oziroma prepišemo obstoječe metode nadrazreda. Z dedovanjem pridobimo vse programske konstrukte nadrazreda, ki jih lahko dopolnimo, ne moremo pa jih odstraniti.

Izpostavimo še, da mora stopnja dostopnosti prepisane metode ostati enaka ali dostopnejša. V kolikor je v nadrazredu označena kot zaščitena oziroma `protected`, mora ostati na tej stopnji ali pa jo smemo odpreti za širšo uporabo, kot javno oziroma `public`. V zasebno oziroma `private` je ne moremo spremeniti, saj bi tako preprečili dostop glede na definicijo metode v nadrazredu.

### Uporaba nadrazredov in podrazredov

Po implementaciji logike v podrazred ustvarimo novo instanco in izpišemo skupno plačo, ki upošteva bonus.

```java
package io.github.e_gradivo.dedovanje;

public class Main {
    public static void main(String[] args) {
        Manager manager = new Manager("Manager 1", 1234.567);
        manager.setBonus(987.65);
        System.out.println("Plača managerja " + manager.getImePriimek() + ": " + manager.getPlaca());
    }
}
```

Ustvarjanje novega objekta in način uporabe se ne razlikuje od ostalih razredov/objektov. Poskusimo ustvariti še tabelo treh zaposlenih in izpišimo njihove plače.

```java
package io.github.e_gradivo.dedovanje;

public class Main {
    public static void main(String[] args) {
        Manager manager = new Manager("Manager 1", 1234.567);
        manager.setBonus(987.65);

        Zaposleni[] zaposleni = new Zaposleni[] {
                manager,
                new Zaposleni("Zaposleni 1", 987.65),
                new Zaposleni("Zaposleni 2", 876.5)
        };

        for (Zaposleni zaposlen : zaposleni) {
            System.out.println("Plača zaposlenega " + zaposlen.getImePriimek() + ": " + zaposlen.getPlaca());
        }
    }
}
```

V okviru tabele smo uporabili že prej ustvarjen objekt `manager`, poleg katerega smo dodali še dve instanci razreda `Zaposleni`. Na koncu smo izpisali ime in plačo posameznega zaposlenega s pomočjo metod `getImePriimek` in `getPlaca`. Po izpisu opazimo, da metoda `getPlaca` vrača pravilen znesek glede na razred objekta - za `Zaposleni` se upošteva osnovna plača, ki jo podamo prek konstruktorja, za `Manager` pa osnovna plača združena še z bonusom, kot smo implementirali logiko v prepisano metodo.

Opazimo, da v obeh primerih kličemo isto metodo `getPlaca`, le da se ta enkrat navezuje na razred `Zaposleni` in drugič na razred `Manager`. Klic metode se vedno opravi na razredu, katerega instanca je objekt. Vemo, da `Manager` **je** `Zaposleni`, zato lahko podrazred vedno uporabimo tudi tam, kjer pravzaprav želimo uporabiti funkcionalnost nadrazreda. Navidezni javanski stroj v ozadju pozna dejanske tipe objektov, zato se vedno proži specifična logika za izbran razred, če ta prepisuje logiko starša. Koncept, ki omogoča referenciranje na več različnih tipov razreda, se imenuje **polimorfizem** _(ang. polymorphism)_. Samodejnemu izbiranju ustrezne metode glede na razred instance v času izvajanja _(ang. runtime)_ pa pravimo **dinamično povezovanje** _(ang. dynamic binding)_.

### Hierarhije dedovanja

Dedovanje razredov ni omejeno na en nivo razširjanja, temveč lahko vsak podrazred uporabimo kot nadrazred njegovemu podrazredu. Na osnovi primera lahko razred `Manager` razširimo v podrazredu `Vodja`. Nabor vseh razredov, ki izhajajo iz enega skupnega nadrazreda imenujemo **hierarhija dedovanja** _(ang. inheritance hierarchy)_. V njej poti od posameznega razreda do njegovih _prednikov_ rečemo **veriga dedovanja** _(ang. inheritance chain)_.

```text
                    +-------------+
                    |             |
                    |  Zaposleni  |
                    |             |
                    +------^------+
                           |
       +-------------------+-------------------+
       |                   |                   |
+------+------+     +------+------+     +------+------+
|             |     |             |     |             |
|   Manager   |     |   Sekretar  |     |  Programer  |
|             |     |             |     |             |
+------^------+     +-------------+     +-------------+
       |
       |
       |
+------+------+
|             |
|    Vodja    |
|             |
+-------------+
```

Od razreda _potomca_ do njegovega oddaljenega _prednika_ običajno obstaja več kot ena veriga. Iz zgornjega prikaza razberemo, da razreda `Sekretar` in `Programer` razširjata razred `Zaposleni`, vendar nimata povezave z razredom `Manager` in obratno. Tak način dedovanja se lahko nadaljuje dokler ne zadostimo smiselni celoti konteksta težave, ki jo rešujemo.

### Polimorfizem _(ang. polymorphism)_

Pravilo po katerem se ravnamo pri odločanju o uporabi tehnike dedovanja je pravilno oblikovanje in interpretacija podatkov, ki jih potrebujemo pri izvajanju programske logike. Relacija "je" zagotavlja, da je vsak objekt določenega podrazreda tudi objekt njegovega nadrazreda. V našem primeru bi lahko zapisali, da je vsak manager tudi zaposleni. Posledično je smiselno, da je razred `Manager` podrazred razreda `Zaposleni`. V obratnem primeru tega ne moremo vedno trditi, saj vsak zaposleni ni tudi manager.

Drugačen način po katerem uvedemo relacijo "je", je **načelo zamenjave** _(ang. substitution principle)_. Omogoči nam, da kadar program pričakuje tip nadrazreda, namesto njega lahko uporabimo podrazred.

```java
Zaposleni zaposleni;
zaposleni = new Zaposleni("Zaposleni 1", 987.65); // ustvarimo objekt pričakovanega nadrazreda
zaposleni = new Manager("Manager 1", 1234.567); // ustvarimo objekt podrazreda - je povsem veljavno
```

V Javi so spremenljivke (oziroma polja) objektov polimorfične. V primeru lahko za spremenljivko `zaposleni` navedemo tako objekt nadrazreda `Zaposleni`, kot tudi objekt podrazreda `Manager` (oziroma kateregakoli drugega, ki v osnovi izhaja iz razreda `Zaposleni`).

```java
Manager manager;
manager = new Manager("Manager 1", 1234.567); // pravilno, saj ustvarimo objekt pričakovanega podatkovnega tipa
manager = new Zaposleni("Zaposleni 1", 987.65); // ni pravilno, saj razred Zaposleni nima ustreznih konstruktov, ki jih uvedemo z razredom Manager
```

Obraten zapis - za spremenljivko `manager` navedemo najprej objekt pričakovanega podatkovnega tipa `Manager`, potem pa ji želimo prirediti objekt razreda `Zaposleni` - ni veljaven, saj s podrazredom `Manager` uvedemo dodatne programske konstrukte, ki jih v razredu `Zaposleni` ni bilo. Posledično ne moremo pričakovati, da bo vedenje objekta razreda `Zaposleni` še vedno ustrezno tudi za njegov podrazred.

Pri uporabi polimorfizma v povezavi s tabelami moramo izpostaviti primer, kjer je potrebna posebna pazljivost.

```java
Manager[] managerji = new Manager[5]; // pravilno
Zaposleni[] zaposleni = managerji; // pravilno
zaposleni[3] = new Zaposleni("Zaposleni 4", 876.5); // izjema pri prirejanju reference objekta, saj izvorni podatkovni tip ni razred Zaposleni
```

Na začetku ustvarimo tabelo razreda `Manager`, ki ji nastavimo poljubno velikost. Zatem se odločimo, da bomo tabeli spremenili podatkovni tip v nadrazred in tako nad elementi uporabljali le vedenje razreda `Zaposleni`. Do te točke je vse pravilno in veljavno, saj kot vemo je vsak podrazred tudi nadrazred in posledično smemo uporabiti tabelo podrazreda kot tabelo nadrazreda. Na težavo pa naletimo pri prirejanju objekta razreda `Zaposleni` na izbran element tabele. Kot vemo vse spremenljivke v Javi v resnici hranijo samo referenco na objekt, ki ga navedemo v času inicializacije. Pri prirejanju spremenljivke `zaposleni` z vrednostjo spremenljivke `managerji` (druga vrstica primera) torej prenesemo samo referenco objekta. Ko želimo v zadnji vrstici primera na tretji indeks tabele nastaviti referenco na objekt razreda `Zaposleni` pri izvajanju naletimo na izjemo. Razlog zanjo se skriva v podrobnostih - spremenljivka `zaposleni` hrani referenco na tabelo razreda `Manager`. Vsak `Zaposleni` ni nujno `Manager`, saj obratna relacija "je" ne obstaja. Posledično želimo preko reference na spremenljivki `zaposleni` na tabelo razreda `Manager` dodati instanco razreda `Zaposleni`, kar pa po opisanem ni mogoče. Za lažjo predstavo našo operacijo ponazorimo še brez vmesne spremembe podatkovnega tipa.

```java
Manager[] managerji = new Manager[5];
managerji[3] = new Zaposleni("Zaposleni 4", 876.5); // ni pravilno, saj nadrazreda ne moremo uporabiti kot element podrazreda
```

V tem primeru na napako naletimo že pri prevajanju. Pri uporabi polimorfizma v povezavi s tabelami moramo biti torej pozorni kadar želimo spreminjati njene elemente, saj ni nujno, da je referenca na katero se sklicujemo istega podatkovnega tipa, kot navedeni podatkovni tip spremenljivke.

### Razumevanje klicev metod

V nadaljevanju bomo predstavili celoten potek klica metode na objektu. Za primer bomo izbrali objekt razreda `Razred`, ki ga bomo poimenovali `objekt`. `Razred` ima implementirano tudi metodo imenovano `metoda`, ki jo smemo klicati s parametri. Klic, ki ga bomo opravili zapišemo kot `objekt.metoda(argumenti)`. Potek klica si sledi ...

1. Prevajalnik najprej preveri deklariran podatkovni tip objekta `objekt` in ime metode. Upoštevati je potrebno, da lahko obstaja več (preobloženih) metod z istim imenom `metoda`, vendar drugačnimi tipi parametrov. Za primer je deklaracija te metode lahko `metoda(int)` ali `metoda(String)`. Prevajalnik preveri vse metode imenovane `metoda` v razredu `Razred` ter poleg tega še vse metode `metoda` v morebitnih nadrazredih razreda `Razred` (z izjemo tistih, ki imajo nastavljeno zasebno stopnjo dostopa). S tem prevajalnik spozna vse možne kandidate za metodo, ki jo mora poklicati.

2. Nadalje prevajalnik preveri tipe argumentov, ki so bili podani ob klicu metode. V kolikor med vsemi metodami imenovanimi `metoda` obstaja edinstvena metoda, katere tipi se ujemajo s parametri klica, jo izbere. Za primer klica `objekt.metoda("Pozdravljeni")` prevajalnik izbere metodo `metoda(String)` in ne metode `metoda(int)`. Če se navežemo na polimorfizem, pri podanih parametrih, ki ustrezajo tako podrazredu, kot nadrazredu, situacija postane težavnejša. V kolikor prevajalnik ne najde ustrezne metode ali jih po spremembi tipov (npr. polimorfizem) obstaja več možnih, potem javi napako. S tem postopkom prevajalnik pozna tako ime, kot tudi tipe parametrov metode, ki jo mora klicati.

3. V kolikor je v metodi uporabljena katera izmed ključnih besed `private`, `static`, `final` ali pa gre v resnici za konstruktor, potem prevajalnik točno ve, katero metodo mora poklicati. Temu pravimo **statično povezovanje** _(ang. static binding)_. V ostalih primerih se mora prevajalnik zanašati neposredno na podatkovni tip objekta `objekt` in uporabiti **dinamično povezovanje** v času izvajanja programa. Slednje drži tudi za našo metodo `metoda(String)`.

4. Pri uporabi dinamičnega povezovanja mora navidezni stroj v času izvajanja programa klicati pravilno metodo z ustreznim dejanskim tipom objekta, na katerega se `objekt` nanaša. Dejanski tip bi lahko bil razred `Podrazred`, ki predstavja podrazred razreda `Razred`. Če ima `Podrazred` definirano metodo `metoda(String)`, potem kliče to metodo. V kolikor to ne drži, navidezni stroj išče naprej v nadrazredu `Razred`. V primeru, da bi imel `Razred` svoj nadrazred, bi se to nadaljevalo še vse do glavnega razreda, ki ni razširjen iz kakšnega drugega.

    Način iskanja metode za vsakokratni klic po dinamičnem povezovanju je po opisanem časovno potraten. V ta namen navidezni stroj že pred dejanskim izvajanjem programa ustvari **tabelo metod** _(ang. method table)_, ki vsebuje vse definicije in dejanske metode, ki jih je možno klicati. Ob klicu tako navidezni stroj le poišče metodo v tabeli metod in jo izvede. V našem primeru za `metoda(String)` je izvorni klic lahko `Podrazred.metoda(String)` ali `Razred.metoda(String)`, pri čemer moramo vedeti, da je v podrazredu možen tudi klic metode iz nadrazreda preko `super.metoda(parameter)`. V kolikor to drži, potem mora navidezni stroj uporabiti tabelo metod za nadrazred.

Naredimo primer še na poljubnem objektu iz zgornjega primera razreda `Zaposleni`, ki smo mu implementirali metodo `getPlaca`. Preverimo potek klica slednje metode na poljubnem objektu tega tipa.

- Metoda ne sprejme nobenih parametrov, zato ne potrebujemo skrbeti za preobložene metode.

- Metoda ne vsebuje katere izmed ključnih besed `private`, `static`, `final`, kar pomeni, da je dinamično povezana.

- Navidezni stroj pripravi tabelo metod za razreda `Zaposleni` in `Manager`. Tabela razreda `Zaposleni` prikaže, da je metoda `getPlaca` poleg metode `getImePriimek` definirana prav v njem:

    `Zaposleni`:
  - `getImePriimek()` -> `Zaposleni.getImePriimek()`
  - `getPlaca()` -> `Zaposleni.getPlaca()`

S tem se postopek iskanja metode zaključi - dodaten korak, ki sicer še sledi napisanemu bomo obrazložili kasneje v tem poglavju.

Za razred `Manager` se tabela metod nekoliko razlikuje, saj je ena metoda prevzeta iz nadrazreda, ena je prepisana, še ena pa je dodana.

`Manager`:

- `getImePriimek()` -> `Zaposleni.getImePriimek()`

- `getPlaca()` -> `Manager.getPlaca()`

- `setBonus(double)` -> `Manager.setBonus(double)`

V času izvajanja bi se klic metode `getPlaca` na poljubnem objektu enega izmed tipov `Zaposleni` ali `Manager` izvedel po naslednjem vrstnem redu:

- Navidezni stroj najprej pridobi tabelo metod za dejanski tip objekta - `Zaposleni` ali `Manager` oz. katerikoli drug podrazred razreda `Zaposleni`.

- Glede na definicijo metode `getPlaca` išče v dejanskem razredu objekta. Ko konča, pozna točno metodo, ki jo uporabi za klic.

- Navidezni stroj pokliče metodo.

Dinamično povezovanje ima zelo pomembno vlogo, saj omogoča, da programe razširimo brez potrebe po spreminjanju obstoječe kode. V kolikor bi dodali nov podrazred `Vodja`, ki razširja razred `Manager`, v obstoječi kodi pa se že navezujemo na katerega izmed njegovih nadrazredov, lahko brez spremembe uporabimo tudi objekte novega tipa namesto nadrazredov. Za primer klica metode `getPlaca` kje v obstoječi kodi, te ne potrebujemo spreminjati, saj vemo, da bo metoda definirana tudi v podrazredu `Vodja`. Tako lahko enostavno dopolnjujemo kodo programa in uvedemo nove podrazrede, ki bodo vedno kompatibilni s kodo njihovih nadrazredov.

### Končni razredi in metode

Občasno se pri implementaciji funkcionalnosti pojavi potreba po preprečevanju razširjanja razredov ali prepisovanja metod. V ta namen obstaja ključna beseda `final`, ki jo uporabimo pri definiciji razreda ali metode. V našem primeru bi lahko ustvarili nov razred `Vodja`, ki razširja razred `Manager`, in mu določili, da je končen.

```java
package io.github.e_gradivo.dedovanje;

public final class Vodja extends Manager {
    public Vodja(String imePriimek, double placa) {
        super(imePriimek, placa);
    }
}
```

Poskusimo ustvariti še podrazred `Nadvodja` razreda `Vodja` ...

```java
package io.github.e_gradivo.dedovanje;

public class Nadvodja extends Vodja {
    public Nadvodja(String imePriimek, double placa) {
        super(imePriimek, placa);
    }
}
```

... in pri prevajanju naletimo na napako, ki nam pove, da je razred `Vodja` že končen.

Podobno, kot za razrede lahko preprečimo prepisovanje metod. Z označevanjem, da je metoda končna je v vseh nadaljnjih podrazredih ne moremo prepisati. To samodejno velja tudi za vse metode končnega razreda.

```java
package io.github.e_gradivo.dedovanje;

public class Zaposleni {
    // ...

    public final String getImePriimek() {
        return imePriimek;
    }

    // ...
}
```

Razlog za označevanje končne metode je jasen - v vseh nadaljnjih podrazredih želimo, da način njenega delovanja ostane predvidljiv oziroma nespremenjen.

Spomnimo se, da smemo tudi polja označiti kot končna, kar pomeni, da jim po inicializaciji ne moremo več spremeniti vrednosti. Ko označimo razred kot končen, to vpliva le na metode (postanejo končne), ne pa tudi na polja.

Dodaten primer končnega razreda je neprimitivni podatkovni tip `String`. Bistveno za določanje njegove končne definicije je referenciranje objekta. Ko ima določena spremenljivka nastavljen podatkovni tip razreda `String`, vedno vemo, da bo referenca objekta kazala na razred `String` in ne kakšnega izmed njegovih podrazredov.

### Pretvorbe

Proces vsiljenega pretvarjanja med dvemi podatkovnimi tipi imenujemo pretvorba _(ang. casting)_. Z njo lahko namenoma naredimo spremembo med kompatibilnimi podatkovnimi tipi. Zapis, ki ga uporabimo so oklepaji, v katerih navedemo pričakovan podatkovni tip ter ga postavimo pred spremenljivko ali vrednost drugega kompatibilnega podatkovnega tipa.

```java
double decimalno = 1234.567;
int celo = (int) decimalno; // uporabimo pretvorbo iz decimalnega v celo število
```

Pretvorbo poleg dela s pritivnimi podatkovnimi tipi uporabljamo tudi pri objektih, kadar želimo spremeniti referenco iz enega razreda na drugega.

```java
Zaposleni[] zaposleni = new Zaposleni[] {
        new Zaposleni("Zaposleni 1", 987.65),
        new Zaposleni("Zaposleni 2", 876.5),
        new Manager("Manager 1", 1234.567)
};
Manager manager = (Manager) zaposleni[2]; // veljavna pretvorba, saj referenca na podanem elementu ustreza razredu Manager
```

Razlog za pretvarjanje tipa objektov je uporaba polne funkcionalnosti razreda, katerega instanca v resnici ta objekt je. Iz primera vidimo, da smo v tabelo razreda `Zaposleni` podali dva objekta pričakovanega razreda ter en objekt podrazreda, ki prav tako ustreza navedenemu razredu. Ob sklicu na element v tabeli vedno dobimo objekt z referenco na razred, ki je podan kot podatkovni tip (v tem primeru je to `Zaposleni`). Posledično moramo za izrabo dodatnih funkcionalnosti, ki jih uvaja podrazred `Manager`, narediti pretvorbo v ta razred. V kolikor bi želeli to isto pretvorbo narediti na kakšnem drugem elementu tabele, bi se pojavila napaka, saj je njuna prvotna referenca na objekt podana z razredom `Zaposleni`.

V izogib napačni pretvorbi nad drugimi referencami na objekt, ki so na primer razreda `Zaposleni`, za preverjanje uporabimo operator `instanceof`. Omogoča nam, da pred dejansko pretvorbo uporabimo pogojni stavek, v katerem se prepričamo, da je prvotna referenca objekta podanega razreda.

```java
Manager manager = new Manager("Manager 1", 1234.567);
manager.setBonus(987.65);

Zaposleni[] zaposleni = new Zaposleni[] {
        new Zaposleni("Zaposleni 1", 987.65),
        new Zaposleni("Zaposleni 2", 876.5),
        manager
};

for (Zaposleni zap : zaposleni) {
    if (zap instanceof Manager) {
        Manager man = (Manager) zap;
        System.out.println(man.getImePriimek() + " je manager s plačo: " + man.getPlaca());
    } else {
        System.out.println(zap.getImePriimek() + " je zaposleni s plačo: " + zap.getPlaca());
    }
}
```

Pretvorbe nad razredi so dovoljene samo znotraj hierarhije dedovanja. Operator `instanceof` lahko uporabimo tudi v povezavi z `null`, saj je privzeta vrednost objekta na spremenljivki oziroma polju prazna. To pomeni, da nima nastavljene reference na objekt pričakovanega podatkovnega tipa.

```java
Zaposleni[] zaposleni = new Zaposleni[] {
        null,
        null,
        new Manager("Manager 1", 1234.567),
};
for (Zaposleni zap : zaposleni) {
    if (zap instanceof Manager) {
        System.out.println(zap.getImePriimek() + " je manager.");
    }
}
```

Uporaba pretvorb ni najbolj zaželena, saj hitro pride do napak pri pisanju kode in posledično izvajanju programa. Iz primera razredov `Zaposleni` in `Manager` ter zgoraj podanih primerov s tabelo in zanko, vidimo, da je pravzaprav funkcionalnost, ki jo uporabljamo v večini že implementirana v nadrazredu `Zaposleni`. Posledično pretvorba pride prav le kadar želimo uporabiti specifično metodo, kot je `setBonus` na razredu `Manager`. V kolikor bi želeli uporabljati metodo `setBonus` tudi na nadrazredu `Zaposleni`, se moramo vprašati ali je oblikovno naša koda zares smiselna in jo temu primerno tudi popraviti.

Pri programiranju moramo stremeti k temu, da pretvorbe in preverjanje s pomočjo operatorja `instanceof` uporabimo čim manjkrat. V kodo namreč dodajo dodatno kompleksnost, ki hitro privede do napak.

### Abstraktni razredi in metode

Ko se po lestvici hierarhije dedovanja premikamo navzgor, razredi postajajo vse splošnejši in bolj abstraktni - so po funkcionalnosti vedno bolj omejeni in vključujejo le najosnovnejše dele. Na neki točki tako lahko namesto njihove usmeritve v reševanje točno določenega problema pomislimo, da tvorijo osnovo tudi za nek drug podoben problem. V našem primeru razreda `Zaposleni` lahko nadalje izločimo podatke in funkcionalnost, ki je vezana na abstraktnejšo entiteto. Zanjo ustvarimo dodaten razred `Oseba`, v enakovreden položaj razredu `Zaposleni` pa lahko ustvarimo razred `Student`. Oba razreda predstavimo kot podrazreda vrhnjega razreda `Oseba`.

```text
           +-------------+
           |             |
           |    Oseba    |
           |             |
           +------^------+
                  |
       +----------+----------+
       |                     |
+------+------+       +------+------+
|             |       |             |
|  Zaposleni  |       |   Student   |
|             |       |             |
+-------------+       +-------------+
```

Razlog za abstrahiranje v tem primeru najdemo pri atributih, saj ima vsaka oseba podatek, kot sta ime in priimek. Ne glede na končni razred, naj bo to `Zaposleni` ali `Student`, vemo, da bomo za njuno identifikacijo potrebovali takšen podatek. Posledično je smiselno, da izvzamemo skupne podatke iz obeh in jih združimo v skupni nadrazred, na vrh hierarhije dedovanja. Poleg imena in priimka dodajmo še metodo `getOpis`, ki bo vračal kratek opis posamezne osebe, glede na tip razreda končnega objekta. V podrazredih implementacija ne bi smela predstavljati težave, medtem ko z nadrazredom `Oseba` brez konteksta v katerem je le-ta predstavljena, ne moremo enostavno dodati opisa.

V izogib implementaciji uvedemo novo ključno besedo `abstract`, ki jo uporabimo tako pri definiciji razreda `Oseba`, kot tudi metode `getOpis`.

```java
package io.github.e_gradivo.dedovanje;

public abstract class Oseba {
    private String imePriimek;

    public Oseba(String imePriimek) {
        this.imePriimek = imePriimek;
    }

    public String getImePriimek() {
        return imePriimek;
    }

    public abstract String getOpis(); // ne potrebujemo implementirati metode
}
```

Kadar želimo imeti vsaj eno izmed metod razreda abstraktno, mora biti abstrakten tudi razred. Kot je prikazano v primeru, sme imeti takšen razred podana tudi polja in druge metode, ki so implementirane. Za označevanje razreda s ključno besedo `abstract` ni nobenega pogoja o vsebovanosti abstraktnih metod, temveč lahko razred kot tak označimo kot abstrakten. To je smiselno, kadar v programu ne želimo imeti instanc tega razreda, temveč razrede s specifično implementacijo in vedenjem. Ustvarjanje objektov abstraktnih razredov namreč ni dovoljeno.

Abstraktne metode služijo namenu prihodnje implementacije - ob ustvarjanju podrazreda, ki razširja abstraktni razred, moramo obvezno implementirati te metode. Za primer lahko vzamemo podrazred `Student` in upoštevamo zahtevano implementacijo.

```java
package io.github.e_gradivo.dedovanje;

public class Student extends Oseba {
    private String smerStudija;

    public Student(String imePriimek, String smerStudija) {
        super(imePriimek);
        this.smerStudija = smerStudija;
    }

    public String getSmerStudija() {
        return this.smerStudija;
    }

    public String getOpis() {
        return String.format(
            "%s je študent smeri %s.",
            this.getImePriimek(),
            this.getSmerStudija()
        );
    }
}
```

V kodi, kjer se navezujemo na objekt razreda `Oseba`, za razliko od instanciiranja še vedno lahko neposredno uporabljamo ta razred. Pri tem so nam za klic na voljo vse metode, ki so definirane s tem razredom, ne glede na njihovo dejansko implementacijo ali abstraktno definicijo.

```java
Oseba student = new Student("Jaz Študent", "računalništvo in informatika");
System.out.println(student.getOpis()); // izpiše opis po dejanski implementaciji v razredu Student
```

Za dokončanje našega primera dopolnimo še razred `Zaposleni`, da bomo imeli zgoraj prikazano hierarhijo dedovanja v celoti implementirano v kodi.

```java
package io.github.e_gradivo.dedovanje;

public class Zaposleni extends Oseba {
    private double placa;

    public Zaposleni(String imePriimek, double placa) {
        super(imePriimek);
        this.placa = placa;
    }

    public double getPlaca() {
        return placa;
    }

    public String getOpis() {
        return String.format(
            "%s je zaposleni s plačo %f.",
            this.getImePriimek(),
            this.getPlaca()
        );
    }
}
```

Uporabimo oba podrazreda še v povezavi s tabelami.

```java
Oseba[] osebe = new Oseba[] {
        new Student("Študent 1", "računalništvo in informatika"),
        new Zaposleni("Zaposleni 1", 1234.567),
};
for (Oseba oseba : osebe) {
    System.out.println(oseba.getOpis());
}
```

Izpostavimo še, da pri klicu `oseba.getOpis()` v zgornjem primeru ne more priti do napake zaradi morebitne neobstoječe implementacije metode (v razredu `Oseba` smo jo označili kot abstraktno). Kadar razširimo kodo abstraktnega razreda, prevajalnik vedno poskrbi za preverjanje obstoja implementacije metod. V nasprotnem primeru se podrazred ne prevede in s tem tudi ne moremo pognati našega programa.

Abstraktni razredi in metode so pomemben koncept v Javi. Z njimi se bomo še dodatno ukvarjali v kasnejšem poglavju.

### Zaščiten dostop

Polja v razredih običajno označimo kot zasebna, metode pa največkrat kot javne. Kot vemo do konstruktov z zasebno stopnjo dostopa izven razreda, kjer jih uvedemo, ne moremo dostopati. Seveda to velja tudi za podrazrede, čeprav mnogokrat ravno iz tam želimo dostopati do njih. Kot rešitev bi lahko uporabili zaščiteno stopnjo dostopa oz. `protected`, kar bi omogočilo neposreden dostop do izbranega konstrukta. Čeprav je to povsem veljavno, moramo vedeti, da `protected` omeji dostop do gradnika na celoten paket v katerem se ta nahaja in ne le na razred ali njegove podrazrede. Uporaba te stopnje dostopa je smiselna kadar je naša koda oblikovana na način, da morebitna uporaba te kode v drugih delih paketa ne more vplivati na nadaljnje spreminjanje naše kode. V kolikor označimo polja kot `protected`, se moramo prav tako zavedati, da v času uporabe razreda, kjer so ta definirana lahko to privede do nepričakovanih operacij oziroma rezultatov tudi znotraj logike razreda.

Uporaba ustreznih stopenj dostopa je torej prepuščena implementatorju kode glede na kontekst in problem, ki ga s programom rešuje. Temu ustrezno je treba uporabiti stopnje dostopa ter premisliti kaj lahko prevelika odprtost v smislu dostopnosti prinese v prihodnje, če bi želeli spremeniti ali dopolniti obstoječo kodo.
