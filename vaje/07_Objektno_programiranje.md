# Objektno programiranje

## Naloga 1

Ustvarite razred `Pes` z lastnostmi `ime`, `pasma`, `starost`, `barva` in vedenjem `opis`, `lajaj`, `sedi`, `spi`. Po klicu metod naj se izpišejo lastnosti in naziv posameznega vedenja (npr. `Floki (pasma: shiba inu, starost: 5 let, barva: oranžna) laja!`).

Rešitev:

<details>
<summary>Pes.java</summary>

```java
class Pes {
  String ime;
  String pasma;
  int starost;
  String barva;

  Pes(String pIme, String pPasma, int pStarost, String pBarva) {
    ime = pIme;
    pasma = pPasma;
    starost = pStarost;
    barva = pBarva;
  }

  String opis() {
    return String.format(
      "%s (pasma: %s, starost: %d let, barva: %s)",
      ime, pasma, starost, barva
    );
  }

  String lajaj() {
    return opis() + " laja!";
  }

  String sedi() {
    return opis() + " sedi!";
  }

  String spi() {
    return opis().concat(" spi!");
  }
}
```

</details>

## Naloga 2

Imamo avto z lastnostmi `znamka`, `model`, `cena`, `voznik` ter funkcionalnostmi `opis`, `nastaviVoznika`, `trenutniVoznik`, `izstopVoznika`, `vzgi`, `ugasni`, `premakni`. V avtomobilu mora biti za delovanje zadnjih treh funkcionalnosti voznik, v nasprotnem primeru naj se izpiše, da avto brez voznika ne deluje. Voznika predstavimo z imenom, številom let imetja vozniškega izpita in starostjo. Njegovo vedenje lahko predstavi s svojim opisom. Prav tako naj funkcionalnosti delujejo po logičnem zaporedju - v kolikor želimo zamenjati voznika, mora prejšnji izstopiti; avto se lahko premakne ali ugasne le če je vžgan; avto lahko vžge samo, če še ni. Ustvarite ustrezne razrede in implementirajte funkcionalnost.

Rešitev:

<details>
<summary>Avto.java</summary>

```java
class Avto {
  String znamka;
  String model;
  int cena;
  Voznik voznik;

  boolean stanje;

  Avto(String vZnamka, String vModel, int vCena) {
    znamka = vZnamka;
    model = vModel;
    cena = vCena;
  }

  String opis() {
    String voz = "ni voznika";
    if (voznik != null) {
      voz = "voznik: " + voznik.opis();
    }
    return String.format(
      "%s %s, %d eur, %s",
      znamka, model, cena, voz
    );
  }

  boolean vzgi() {
    if (stanje || voznik == null) {
      return false;
    }
    stanje = true;
    return stanje;
  }

  boolean ugasni() {
    if (stanje || voznik != null) {
      stanje = false;
      return true;
    }
    return false;
  }

  boolean premakni() {
    return stanje && voznik != null;
  }

  void nastaviVoznika(Voznik v) {
    voznik = v;
  }

  Voznik trenutniVoznik() {
    return voznik;
  }

  boolean izstopVoznika() {
    if (!stanje) {
      voznik = null;
      return true;
    }
    return false;
  }
}
```

</details>

<details>
<summary>Voznik.java</summary>

```java
class Voznik {
  String ime;
  int vozniskoLet;
  int starostLet;

  Voznik(String vIme, int vVozniskoLet, int vStarostLet) {
    ime = vIme;
    vozniskoLet = vVozniskoLet;
    starostLet = vStarostLet;
  }

  String opis() {
    return String.format(
      "%s, voznisko dovoljenje let: %d, starost let: %d",
      ime, vozniskoLet, starostLet
    );
  }
}
```

</details>

## Naloga 3

Obstaja več različnih igralnih kock, na primer s 6, 12 in 20 ploskvami. Ustvarite razred, ki bo sprejel število ploskev in imel metode `vrednosti` (izpiše vse ploskve in število pik na njih), `metanje` (vrne naključno število pik glede na ploskve kocke), `zaporedje(int poskusov)` (vrne tabelo naključnih vrednosti števila pik v velikosti poskusov). Nato ustvarite objekte za vse tri omenjene igralne kocke in izpišite vrednosti po izvedbi vseh metod - uporabite tabele kamor shranite število ploskev kock in nato s pomočjo zanke (brez ponavljanja kode) dokončajte ustvarjanje in izpis.

Rešitev:

<details>
<summary>IgralnaKocka.java</summary>

```java
import java.util.Random;

class IgralnaKocka {
  int ploskev;
  Random rand = new Random();

  IgralnaKocka(int vPloskev) {
    ploskev = vPloskev;
  }

  void vrednosti() {
    for (int i = 1; i <= ploskev; i++) {
      System.out.printf("Ploskev %d. ima število pik: %d\n", i, i);
    }
  }

  int metanje() {
    return rand.nextInt(ploskev) + 1;
  }

  int[] zaporedje(int poskusov) {
    int[] poskusi = new int[poskusov];
    for (int i = 0; i < poskusov; i++) {
      poskusi[i] = metanje();
    }
    return poskusi;
  }
}
```

</details>

<details>
<summary>Naloga3.java</summary>

```java
class Naloga3 {
    public static void main(String[] args) {
        int[] ploskve = { 6, 12, 20 };
        for (int ploskev : ploskve) {
            System.out.println("Kocka ploskev: " + ploskev);
            IgralnaKocka ik = new IgralnaKocka(ploskev);
            ik.vrednosti();

            System.out.println("Število pik na kocki: " + ik.metanje());

            int[] zaporedje = ik.zaporedje(5);
            for (int v : zaporedje) {
                System.out.println("Poskus je vrnil vrednost/število pik: " + v);
            }
            System.out.println("--------------------------------------");
        }
    }
}
```

</details>

## Naloga 4

Ustvarite razrede za pravokotnik, kvadrat in trikotnik. Dolžine stranic podajte preko konstruktorja, razred pa naj vsebuje metode `stranice` (vrne dolžine posamezne stranice), `obseg` (vrne obseg izbranega lika) in `ploscina` (vrne ploščino izbranega lika). Nato uporabniku omogočite vnos poljubnih vrednosti - lik ter dolžine stranic in ime metode, katere vrednost se izpiše.

Vhod:

```text
pravokotnik
2
4
ploščina
```

Izhod:

```text
Ploščina pravokotnika s stranicami a=2, b=4 je 8.
```

Rešitev:

<details>
<summary>Pravokotnik.java</summary>

```java
class Pravokotnik {
  int a;
  int b;

  Pravokotnik(int vhodA, int vhodB) {
    a = vhodA;
    b = vhodB;
  }

  void stranice() {
    System.out.println(
      String.format(
        "a = %d, b = %d",
        a, b
      )
    );
  }

  int obseg() {
    return 2*a + 2*b;
  }

  int ploscina() {
    return a*b;
  }
}
```

</details>

<details>
<summary>Kvadrat.java</summary>

```java
class Kvadrat {
    int stranica;

    Kvadrat(int vStranica) {
        stranica = vStranica;
    }

    String stranice() {
        return "a = " + stranica;
    }

    int obseg() {
        return 4*stranica;
    }

    int ploscina() {
        return stranica*stranica;
    }
}
```

</details>

<details>
<summary>Trikotnik.java</summary>

```java
class Trikotnik {
    // Enakostranični trikotnik

    int stranica;

    Trikotnik(int vStranica) {
        stranica = vStranica;
    }

    String stranice() {
        return "a = " + stranica;
    }

    int obseg() {
        return stranica*3;
    }

    double ploscina() {
        return (stranica*stranica*Math.sqrt(3))/4;
    }
}
```

</details>

<details>
<summary>Naloga4.java</summary>

```java
import java.util.Scanner;

class Naloga4 {
    public static void main(String[] args) {
        Scanner scn = new Scanner(System.in);
        System.out.println("Vnesite lik:");
        String vnos = scn.nextLine();

        if (vnos.equals("pravokotnik")) {
            pravokotnik();
        } else if (vnos.equals("kvadrat")) {
            kvadrat();
        } else if (vnos.equals("trikotnik")) {
            trikotnik();
        } else {
            System.out.println("Napacen vnos!");
        }
    }

    public static void izpis(String vrsta, String vrednost, String stranice) {
        System.out.println(
            vrsta + " pravokotnika s stranicami " +
            stranice + (vrednost != null ? " je " + vrednost: "") + "." 
        );
    }

    public static void pravokotnik() {
        Scanner scn = new Scanner(System.in);
        String vnos = scn.nextLine();
        System.out.println("Vpisite stranice pravoktonika:");

        int stranica1 = Integer.parseInt(scn.nextLine());
        int stranica2 = Integer.parseInt(scn.nextLine());

        Pravokotnik pr = new Pravokotnik(stranica1, stranica2);

        System.out.println("Vpisite vrsto racuna:");
        String vrsta = scn.nextLine();

        if (vrsta.equals("stranice")) {
            izpis("Stranice", null, pr.stranice());
        } else if (vrsta.equals("obseg")) {
            izpis("Obseg", pr.obseg() + "", pr.stranice());
        } else if (vrsta.equals("ploscina")) {
            izpis("Ploscina", pr.ploscina() + "", pr.stranice());
        } else {
            System.out.println("Vnesena vrsta ne obstaja!");
        }
    }

    public static void kvadrat() {
        Scanner scn = new Scanner(System.in);
        String vnos = scn.nextLine();
        System.out.println("Vpisite stranico kvadrata:");

        int stranica1 = Integer.parseInt(scn.nextLine());

        Kvadrat kv = new Kvadrat(stranica1);

        System.out.println("Vpisite vrsto racuna:");
        String vrsta = scn.nextLine();

        if (vrsta.equals("stranice")) {
            izpis("Stranice", null, kv.stranice());
        } else if (vrsta.equals("obseg")) {
            izpis("Obseg", kv.obseg() + "", kv.stranice());
        } else if (vrsta.equals("ploscina")) {
            izpis("Ploscina", kv.ploscina() + "", kv.stranice());
        } else {
            System.out.println("Vnesena vrsta ne obstaja!");
        }
    }

    public static void trikotnik() {
        Scanner scn = new Scanner(System.in);
        String vnos = scn.nextLine();
        System.out.println("Vpisite stranico trikotnika:");

        int stranica1 = Integer.parseInt(scn.nextLine());

        Trikotnik tr = new Trikotnik(stranica1);

        System.out.println("Vpisite vrsto racuna:");
        String vrsta = scn.nextLine();

        if (vrsta.equals("stranice")) {
            izpis("Stranice", null, tr.stranice());
        } else if (vrsta.equals("obseg")){
            izpis("Obseg", tr.obseg() + "", tr.stranice());
        } else if (vrsta.equals("ploscina")) {
            izpis("Ploscina", tr.ploscina() + "", tr.stranice());
        } else {
            System.out.println("Vnesena vrsta ne obstaja!");
        }
    }
}
```

</details>

## Naloga 5

Ustvarite razreda za kvader in kocko. Dolžino, širino in višino podajte preko konstruktorja, razred pa naj vsebuje metode `podatki` (vrne dolžino, širino in višino), `povrsina` (vrne površino izbranega geometrijskega telesa), `prostornina` (vrne prostornino izbranega geometrijskega telesa), `vsebuje(Kvader kvader)` (vrne logično vrednost - v kolikor lahko podano geometrijsko telo v parametru glede na podatke spravimo vanj). Nato uporabniku omogočite vnos poljubnih vrednosti za dva ista geometrijska telesa in izpišite vse podatke, ki jih vračajo metode.

Vhod:

```text
kvader
2
2
2
4
4
4
```

Izhod:

```text
Kvader 1 | Dolžina: 2, Širina: 2, Višina: 2 | Površina: 24, Prostornina: 8 | Vsebuje naslednjega: ne
Kvader 2 | Dolžina: 4, Širina: 4, Višina: 4 | Površina: 192, Prostornina: 64 | Vsebuje prejšnjega: da
```

Rešitev:

<details>
<summary>Kvader.java</summary>

```java
class Kvader {
    int dolzina;
    int visina;
    int sirina;

    Kvader(int vDolzina, int vVisina, int vSirina) {
        dolzina = vDolzina;
        visina = vVisina;
        sirina = vSirina;
    }

    String podatki() {
        return "sirina = " + sirina +
            ", visina = " + visina +
            ", dolzina = " + dolzina;
    }

    int povrsina() {
        return 2*dolzina*sirina + 2*dolzina*visina + 2*sirina*visina;

    }

    int prostornina() {
        return dolzina*visina*sirina;
    }

    boolean vsebuje(Kvader kvader) {
        return dolzina>kvader.dolzina && sirina>kvader.sirina && visina>kvader.visina;

    }
}
```

</details>

<details>
<summary>Kocka.java</summary>

```java
class Kocka {
    int a;

    Kocka(int vA) {
        a = vA;
    }

    String podatki() {
        return "sirina = " + a +
            ", visina = " + a +
            ", dolzina = " + a;
    }

    int povrsina() {
        return 6*a*a;

    }

    int prostornina() {
        return a*a*a;
    }

    boolean vsebuje(Kocka kocka) {
        return a>kocka.a;
    }
}
```

</details>

<details>
<summary>Naloga5.java</summary>

```java
import java.util.Scanner;

class Naloga5 {
    public static void main(String[] args){
        Kvader[] kvadri = new Kvader[2];
        Scanner sc = new Scanner(System.in);
        for(int i = 0; i < kvadri.length; i++) {
            System.out.print("Dolžina: ");
            int dolzina= sc.nextInt();
            System.out.print("Širina: ");
            int sirina= sc.nextInt();
            System.out.print("Višina: ");
            int visina= sc.nextInt();
            kvadri[i] = new Kvader(dolzina, visina, sirina);

        }
        for(int i = 0; i < kvadri.length; i++) {
            Kvader kv = kvadri[i];
            String izpis = "Kvader " + (i+1) + " " + kv.podatki() +
                " | Površina: " + kv.povrsina() +
                " Prostornina: " + kv.prostornina();
            if (i == 0) {
                izpis += " | Vsebuje naslednjega: " + (kv.vsebuje(kvadri[i+1]) ? "da" : "ne");
            } else {
                izpis += " | Vsebuje prejšnjega: " + (kv.vsebuje(kvadri[i-1]) ? "da" : "ne");
            }
            System.out.println(izpis);
        }
    }
}
```

</details>

---

## Naloga 6

Želimo sestaviti računalnik po posameznih komponentah in izračunati skupno končno ceno. Ustvarite razred `Racunalnik` s pripadajočimi lastnostmi (posamezne komponente), katere je možno nastaviti z `nastavi[komponenta](Komponenta komponenta)` in odstraniti z `odstrani[komponenta](Komponenta komponenta)` (oznako `[komponenta]` nadomestite z imenom lasnosti) in vedenjem `skupnaCena`, `skupnaCena(double popust)`, `izpisKomponent` (izpiše posamezne komponente s predpono imena komponente in nato nazivom artikla), `kosarica` (izpiše naziv artikla in ceno). Ustvarite še vsebovani razred `Komponenta`, ki hrani naziv artikla in ceno ter ima metodi `vrniNaziv` in `vrniCeno`. Sestavite ustrezne objekte in izpišite komponente, skupno ceno in skupno ceno z 10% popustom.

## Naloga 7

V organizaciji imamo zaposlene, katerih število se zaradi obsega dela povečuje dnevno. Ustvarite razred `Organizacija`, ki hrani tabelo zaposlenih z vedenjem `steviloZaposlenih`, `dodajZaposlenega(Zaposleni zaposleni)`, `odstraniZaposlenega(Zaposleni zaposleni)`, `idZaposlenega(Zaposleni zaposleni)`, `skupajPlace` (izračuna skupni mesečni znesek plač) in `izpisiZaposlene` (izpiše ime vsakega zaposlenega in plačo). Ima naj prazen konstruktor, konstruktor, ki sprejme začetno število zaposlenih in konstruktor, ki sprejme začetne zaposlene. Ustvarite razred `Zaposleni`, ki hrani ime in priimek zaposlenega ter njegovo mesečno plačo, z vedenjem `vrniIme` in `vrniPlaco`. Sestavite ustrezne objekte, dodajte 3 privzete zaposlene in omogočite uporabniku vnos dodatnih (pred oz. po vnosu posameznega ga vprašajte, če želi nadaljevati z dodajanjem).

## Naloga 8

Imamo šolski urnik, na katerem najdemo predmete v časovnem zaporedju po dnevih. Predpostavimo, da urnik vključuje pet dni (ponedeljek - petek, označimo z indeksi 0 - 4), na katere lahko dodamo ure predmetov (upoštevamo, da ima vsak dan največ 10 ur). Vsaka ura je definirana iz časa začetka ter predmeta, ki se v tem času izvaja. Vsi predmeti so tudi shranjeni na urniku. Napišite vse tri razrede z ustreznimi lastnostmi za pričakovano delovanje:

- Urnik: `Urnik(int steviloPredmetov)`, `Urnik(Predmet[] predmeti)`, `dodajPredmet(Predmet predmet)`, `odstraniPredmet(Predmet predmet)`, `pridobiPredmet(String okrajsava)`, `zbirkaPredmetov`, `dodajUro(int dan, Ura ura)`, `odstraniUro(int dan, String ura)`, `zbirkaUr(int dan)`, `izpisiVse`
- Ura: `Ura(String cas, Predmet predmet)`, `vrniCas`, `vrniPredmet`
- Predmet: `Predmet(String okrajsava, String ime)`, `Predmet(String okrajsava, String ime, String opis)`, `vrniOkrajsavo`, `vrniIme`, `vrniOpis`

Sestavite svoj urnik in izpišite ure po dnevih. Za proste ure naj obstaja predmet z imenom `Prosto` in okrajšavo `/`.

## Naloga 9

Mobilni operater ponuja tri različne pakete, ki vključujejo specifično velikost enot za klice, sporočila in prenos podatkov. Uporabniki imajo različne zahteve po enotah, okvirno pa vedo koliko jih mesečno porabijo. Ustvarite razred `Operater`, ki hrani prostor za tri pakete in ima vedenje `izpisiPakete` (izpiše imena paketov in število posameznih enot) ter `ustrezenPaket(Uporabnik uporabnik)` (primerja enote uporabnika z enotami paketa in izbere najbolj ustreznega glede na število enot in ceno). Ustvarite razred `Paket`, ki hrani število posameznih enot za klice, sporočila in prenos podatkov ter ima vedenje `ustreza(int pogovoriEnot, int sporocilaEnot, int prenosPodatkovEnot)` (vrača logično vrednost, če paket ustreza podanemu številu enot) in `ustreza(Paket paket)` (vrača logično vrednost, če je število enot paketa, ki ga podamo kot parameter manjše ali enako trenutnemu). Ustvarite razred `Uporabnik` z lastnostmi ime in priimek ter predvidenim številom porabe enot. Ima naj metode `vrniIme`, `vrniPogovoriEnot`, `vrniSporocilaEnot` in `vrniPrenosPodatkovEnot`. Sestavite ustrezne objekte in ustvarite 3 uporabnike, kjer dva ustrezata predvidenim paketom, en pa nobenemu.

## Naloga 10

Napišite razred `Oseba`, ki hrani ime, priimek, spol, leto rojstva ter referenco na očeta in mati, ki sta predstavljena z istim razredom. Razred naj vsebuje konstruktor `Oseba(String ime, String priimek, char spol, int letoRojstva, Oseba oce, Oseba mati)` ter metode:

- `vrniIme`: vrne ime in priimek osebe
- `starost(int leto)`: vrne starost izračunano glede na vhodni parameter
- `toString`: vrne kratek opis v obliki: `Ime Priimek, M, 2000`
- `jeStarejsaOd(Oseba oseba)`: vrne logično vrednost po primerjavi starosti trenutne osebe in osebe podane v parametru
- `jeBratAliSestraOd(Oseba oseba)`: vrne logično vrednost glede na ustreznost prednikov
- `imeOceta`: vrne ime očeta
- `imeMatere`: vrne ime matere

Sestavite ustrezne objekte za družinsko drevo sestavljeno iz dveh različnih vrhnjih družin in eno skupno, ki je izpeljana iz vrhnjih.
