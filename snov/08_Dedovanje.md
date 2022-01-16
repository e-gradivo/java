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

V podrazredu torej na nek način označujemo samo spremembe od nadrazreda, ki ga razširjamo. Upoštevati moramo, da je v nadrazred vključena le splošna logika, ki je skupna vsem nadaljnjim podrazredom. Specifične funkcionalnosti, ki so namenjene le točno določenemu delu našega programa torej uvrstimo v podrazred. S tem omogočimo vzpostavitev hierarhije za logične dele programa in se v primeru kasnejših potreb po dopolnitvi programske logike navežemo na tistega, ki ji najbolj ustreza. V naprej pa mnogokrat ne moremo predvideti možnih razširitev programa, zato je v okviru objektnega programiranja ustaljena praksa izločanja skupne kode v lastni razred in prestrukturiranja logike. To opravimo, ko je problem programa natančneje definiran in s tem kodo oblikujemo v bolj smiselno celoto. Pri tem eno ključih vlog igra prav koncept dedovanja.

### Prepisovanje metod

Kadar želimo spremeniti logiko določene metode v podrazredu, jo moramo prepisati. V primeru razreda `Manager` je takšna metoda `getPlaca`, saj po razširanju nadrazreda vključuje le osnovno logiko vračanja plače, brez upoštevanja bonusa. Prepisovanje metode opravimo tako, da njeno definicijo v celoti prepišemo, kot je v nadrazredu, nato pa v blok zapišemo podrazredu lastno logiko.

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
