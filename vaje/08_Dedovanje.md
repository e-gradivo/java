# Dedovanje

## Naloga 1 (nadrazredi, podrazredi)

Napišite razreda, ki predstavljata lik oziroma geometrijsko telo z naslednjim vedenjem:

- Krog: `Krog(double polmer)`, `getPolmer`, `getObseg`, `getPloscina`, `toString` (vrne niz v obliki `Krog s polmerom: [polmer]`, pri čemer `[polmer]` zamenjate z dejansko vrednostjo polja `polmer` in dodate poljubno mersko enoto)
- Valj: `Valj(double visina, double polmer)`, `getVisina`, `getProstornina`, `getPovrsina`, `toString` (vrne niz v obliki `Valj z višino [visina] in polmerom [polmer].`, pri čemer `[visina]` in `[polmer]` zamenjate s pripadajočo vrednostjo istoimenskega polja in dodate poljubno mersko enoto)

Upoštevajte koncept dedovanja in ustrezno razširite izbran razred. V paketu nato ustvarite vstopno točko in na primeru uporabite oba ustvarjena razreda.

Rešitev:

<details>
<summary>Krog.java</summary>

```java
package io.github.e_gradivo.dedovanje.naloga1;

public class Krog {
    private double polmer;

    public Krog(double polmer) {
        this.polmer = polmer;
    }

    public double getPolmer() {
        return polmer;
    }

    public double getObseg() {
        return polmer * 2 * Math.PI;
    }

    public double getPloscina() {
        return Math.pow(polmer, 2) * Math.PI;
    }

    public String toString() {
        return String.format("Krog s polmerom: %f", polmer);
    }
}
```

</details>

<details>
<summary>Valj.java</summary>

```java
package io.github.e_gradivo.dedovanje.naloga1;

public class Valj extends Krog {
    private double visina;

    public Valj(double visina, double polmer) {
        super(polmer);
        this.visina = visina;
    }

    public double getVisina() {
        return visina;
    }

    public double getProstornina() {
        return visina * Math.pow(getPolmer(), 2) * Math.PI;
    }

    public double getPovrsina() {
        return 2 * Math.pow(getPolmer(), 2) * Math.PI + visina * 2 * Math.PI * getPolmer();
    }

    public String toString() {
        return String.format("Valj z visino %f in polmerom %f", visina, getPolmer());
    }
}
```

</details>

<details>
<summary>Vstopni.java</summary>

```java
package io.github.e_gradivo.dedovanje.naloga1;

class Vstopni {
    public static void main(String[] args) {
        Krog krog = new Krog(4.5);
        Valj valj = new Valj(12.67, 4.5);

        System.out.println(krog.toString());
        System.out.println(valj.toString());
    }
}
```

</details>

## Naloga 2 (nadrazredi, podrazredi)

Ustvarite programska gradnika za predstavitev točk v dvodimenzionalnem in trodimenzionalnem kartezičnem koordinatnem sistemu, pri čemer drugi nadgrajuje funkcionalnost prvega. Razreda poimenujte `Tocka2D` in `Tocka3D`. Oba naj imata implementiran prazen konstruktor in konstruktor z vsemi podatki, ki definirajo točko ter pripadajoče nastavljalce in pridobivalce. Poleg tega naj ob klicu metode `toString` vračata predstavitev razdalj do točke po posamezni osi v oklepajih.

Program nadgradite z dodatnima razredoma, ki vključujeta tabelo za pripadajočo dimenzijo točke in ju poimenujte `Koordinate2D` in `Koordinate3D`. Namenjena naj bosta kot osnova za lik `Kvadrat` in geometrijsko telo `Kocka`. Napišite konstruktor, ki na vhodu sprejme objekt pripadajočih koordinat, pri čemer predpostavite, da so podani podatki pravilni. Za kvadrat implementirajte metode `getStranica`, `getObseg` in `getPloscina`, za kocko pa `getRob`, `getProstornina` in `getPovrsina`.

V paketu ustvarite vstopno točko in na primeru uporabite vse ustvarjene razrede.

Rešitev:

<details>
<summary>Tocka2D.java</summary>

```java
package io.github.e_gradivo.dedovanje.naloga2;

public class Tocka2D {
    private int x;
    private int y;

    public Tocka2D(int x, int y) {
        this.x = x;
        this.y = y;
    }

    public String toString() {
        return String.format("x: %d, y: %d", x, y);
    }

    public int getX() {
        return x;
    }

    public int getY() {
        return y;
    }
}
```

</details>

<details>
<summary>Tocka3D.java</summary>

```java
package io.github.e_gradivo.dedovanje.naloga2;

public class Tocka3D extends Tocka2D {
    private int z;

    public Tocka3D(int x, int y, int z) {
        super(x, y);
        this.z = z;
    }

    public int getZ() {
        return z;
    }

    public String toString() {
        return String.format("x: %d, y: %d, z: %d", getX(), getY(), getZ());
    }
}
```

</details>

<details>
<summary>Vstopni.java</summary>

```java
package io.github.e_gradivo.dedovanje.naloga2;

public class Vstopni {
    public static void main(String[] args) {
        int x = 2;
        int y = 2;
        int z = 2;

        Tocka2D tocka = new Tocka2D(x, y);
        System.out.println(tocka.toString());

        Tocka3D tockadve = new Tocka3D(x, y, z);
        System.out.println(tockadve.toString());
    }
}
```

</details>

## Naloga 3 (prepisovanje metod)

Napišite programske gradnike za namen uporabe koncepta dedovanja v kontekstu cestnih vinjet. V okviru naloge obstajajo tri različne vinjete - tedenska (7 dni), mesečna (28 dni) in letna (336 dni). Glede na obdobje, ki ga predstavljajo je ustrezna tudi cena:

- Tedenska: 20 enot
- Mesečna: 80 enot _(tedenska * 4)_
- Letna: 800 enot _(mesečna * 12 - 20% popust)_

Ustvarite pripadajoče razrede in v konstruktorju pridobite datum začetka veljavnosti vinjete. Implementirajte metode `getNaziv`, `getZacetekVeljavnosti`, `getTrajanjeDni`, `getCena` in `toString` (vrača opis v obliki `[naziv], začetek veljavnosti [datum], trajanje: [trajanje dni] dni, cena: [cena] enot`, pri čemer podatke v oglatih oklepajih zamenjajte s klici pripadajočih metod). Pri obeh nadaljnjih razredih glede na časovno obdobje razširite predhodnega.

V paketu ustvarite vstopno točko in uporabite vse ustvarjene razrede.

Rešitev:

<details>
<summary>Vinjeta.java</summary>

```java
package io.github.e_gradivo.dedovanje.naloga3;

public class Vinjeta {
    private String naziv;
    private String zacetekVeljavnosti;
    private int trajanje;

    public Vinjeta(String naziv, String zacetekVeljavnosti, int trajanje) {
        this.naziv = naziv;
        this.zacetekVeljavnosti = zacetekVeljavnosti;
        this.trajanje = trajanje;
    }

    public String getNaziv() {
        return naziv;
    }

    public String getZacetekVeljavnosti() {
        return zacetekVeljavnosti;
    }

    public int getTrajanjeDni() {
        return trajanje;
    }

    public double getCena() {
        return -1;
    }

    public String toString() {
        return String.format(
                "%s, zacetek veljavnosti %s, trajanje: %d dni, %f enot",
                naziv,
                zacetekVeljavnosti,
                trajanje,
                getCena());
    }
}
```

</details>

<details>
<summary>Tedenska.java</summary>

```java
package io.github.e_gradivo.dedovanje.naloga3;

public class Tedenska extends Vinjeta {
    public Tedenska(String zacetekVeljavnosti) {
        super("Tedenska", zacetekVeljavnosti, 7);
    }

    protected Tedenska(String naziv, String zacetekVeljavnosti, int trajanje) {
        super(naziv, zacetekVeljavnosti, trajanje);
    }

    public double getCena() {
        return 20;
    }
}
```

</details>

<details>
<summary>Mesecna.java</summary>

```java
package io.github.e_gradivo.dedovanje.naloga3;

public class Mesecna extends Tedenska {
    public Mesecna(String zacetekVeljavnosti) {
        super("Mesecna", zacetekVeljavnosti, 28);
    }

    protected Mesecna(String naziv, String zacetekVeljavnosti, int trajanje) {
        super(naziv, zacetekVeljavnosti, trajanje);
    }

    public double getCena() {
        return super.getCena() * 4;
    }
}
```

</details>

<details>
<summary>Letna.java</summary>

```java
package io.github.e_gradivo.dedovanje.naloga3;

public class Letna extends Mesecna {
    public Letna(String zacetekVeljavnosti) {
        super("Letna", zacetekVeljavnosti, 336);
    }

    protected Letna(String naziv, String zacetekVeljavnosti, int trajanje) {
        super(naziv, zacetekVeljavnosti, trajanje);
    }

    public double getCena() {
        double cena1 = super.getCena() * 12;
        return cena1 - 0.2 * cena1;
    }
}
```

</details>

<details>
<summary>Vstopni.java</summary>

```java
package io.github.e_gradivo.dedovanje.naloga3;

class Vstopni {
    public static void main(String[] args) {
        Tedenska tedenska = new Tedenska("25.3.2022");
        Mesecna mesecna = new Mesecna("25.3.2022");
        Letna letna = new Letna("25.3.2022");

        System.out.println(tedenska.toString());
        System.out.println(mesecna.toString());
        System.out.println(letna.toString());

    }
}
```

</details>

## Naloga 4 (polimorfizem)

Ustvarite razrede za hierarhijo dedovanja kategorizacije cest. Obstajajo naslednje kategorije:

- Avtocesta (AC)
- Hitra cesta (HC)
- Glavna cesta (1. red: G1, 2. red: G2)
- Regionalna cesta (1. red: R1, 2. red: R2, 3. red: R3)

Vsako izmed cest ločimo po kategoriji, pri čemer moramo upoštevati še morebitni red, kateremu pripadajo. Podatki, ki jih želimo zajeti za predstavitev ceste so številka ceste, začetek in konec, potek in dolžina v kilometrih. Pridobite jih preko konstruktorja ter izpostavite preko pridobivalcev.

Vsak razred kategorije cest naj izpostavlja še naslednje metode `getKategorija`, `imaRed`, `getRed`. V paketu ustvarite vstopno točko v kateri inicializirajte tabelo začetnega razreda in vanjo dodajte več vrst cest, predstavljenih z objekti različnih razredov. V pomoč vam je lahko spodnja tabela:

| kategorija | številka ceste | začetek | konec | potek | dolžina (km) |
| -- | -- | -- | -- | -- | -- |
| AC | A1 | meja R Avstrija | HC H5 | Šentilj–Dragučova–Maribor–Slivnica–Celje–Trojane–Ljubljana (Zadobrova–Malence–Kozarje)–Postojna–Divača–Črni Kal–Srmin | 245,270
| HC | H3 | AC A1 | AC A2 | Ljubljana (Zadobrova–Tomačevo–Koseze) | 10,220
| G1 | 8 | R1-211 | HC H3 | Ljubljana (Šentvid – obvoznica) | 2,900
| G2 | 108 | G2-104 | G1-5 | Ljubljana (Črnuče)–Litija–Hrastnik–Zidani Most | 64,663
| R1 | 206 | R1-201 | R1-203 | Kranjska Gora (Ruska cesta)–Vršič–Trenta–Bovec | 43,630
| R2 | 412 | R1-210 | R1-210 | Naklo (Kranj zahod)–Kranj–Kranj (Labore) | 5,044
| R3 | 641 | R2-407 | R2-409 | Ljubljanica–Brezovica | 23,456

Nato s pomočjo zanke naredite izpis vseh cest v tabeli in njihovih lastnosti.

## Naloga 5 (polimorfizem)

Ustvarite programske gradnike za hierarhijo dedovanja različnih vrst kablov. V nalogi bomo zajeli naslednje:

- Električni kabel _(vhodi/izhodi: C13, C14, Type-A, Type-B, Type-C)_
- Mrežni kabel _(vhodi/izhodi: UTP, SFP, LC, SC)_
- USB kabel _(vhodi/izhodi: Type-A, Type-B, Type-C)_
- Video kabel _(vhodi/izhodi: VGA, HDMI, DVI, DMS-59)_
- Audio kabel _(vhodi/izhodi: ADAT, XLR, BNC, TS, TRS)_

Vsak izmed splošnih razredov naj ima metodo `getVrsta` in `getOpisUporabe`. Vsakemu kablu določimo vhodni in izhodni konektor in dolžino v metrih. Te podatke pridobite preko konstruktorja in izpostavite preko pripadajočih pridobivalcev.

V paketu ustvarite vstopno točko v kateri inicializirajte tabelo začetnega razreda in vanjo dodajte več različnih vrst kablov. S pomočjo zanke naredite izpis vseh z njihovimi lastnostmi.

## Naloga 6 (končni razredi in metode)

Napišite razrede za hierarhijo dedovanja košarkarskega moštva, ki vključuje igralce, selektorja in njegove pomočnike, trenerje, zdravnike in fizioterapevte. Vsi razredi omenjenih nazivov z izjemo igralca naj bodo končni, igralci pa naj bodo naprej predstavljeni po njihovih končnih igralnih mestih ter vedenjem, ki odraža posamično tekmo:

- Organizator (številka ena): `Organizator(String imePriimek, int stevilkaDresa)`, `setSteviloPodaj(int steviloPodaj)`, `getSteviloPodaj`, `setSteviloAsistenc(int steviloAsistenc)`, `getSteviloAsistenc`, `setSteviloKosev(int steviloKosev)`, `getStevilkaPozicije`
- Branilec (številka dve): `Branilec(String imePriimek, int stevilkaDresa)`, `setSteviloTrojk(int steviloTrojk)`, `getSteviloTrojk`, `setSteviloPodaj(int steviloPodaj)`, `getSteviloPodaj`, `getStevilkaPozicije`
- Krilo (številka tri): `Krilo(String imePriimek, int stevilkaDresa)`, `setSteviloOdvzetihZog(int steviloOdvzetihZog)`, `getSteviloOdvzetihZog`, `setSteviloPobranihZog(int steviloPobranihZog)`, `getSteviloPobranihZog`, `getStevilkaPozicije`
- Krilni center (številka štiri): `KrilniCenter(String imePriimek, int stevilkaDresa)`, `setSteviloPobranihZog(int steviloPobranihZog)`, `getSteviloPobranihZog`, `setSteviloTrojk(int steviloTrojk)`, `getSteviloTrojk`, `getStevilkaPozicije`
- Center (številka pet): `Center(String imePriimek, int stevilkaDresa)`, `setSteviloBlokad(int steviloBlokad)`, `getSteviloBlokad`, `setSteviloKosev(int steviloKosev)`, `getSteviloKosev`, `getStevilkaPozicije`

Implementirajte zahtevano vedenje in uporabite ustvarjene razrede za predstavitev poljubne ekipe. Slednjo dodajte v vstopni razred paketa in na poljuben način naredite izpis v namen njene predstavitve.

## Naloga 7 (končni razredi in metode)

Ustvarite programske gradnike za hierarhijo dedovanja mobilnih in internetnih naročniških paketov. Veriga dedovanja do vsakega zadnjega razreda naj bo dolga točno dva nivoja, vsak zadnji razred pa naj bo tudi končen. Vedenje na začetnem nivoju naj bo določeno na splošno glede na osnove, ki jih zajema prvi nivo. Slednji naj bo specifično določen z naslednjimi operacijami:

- MobilniPaket: `MobilniPaket(String naziv, double narocnina, double minute, double smsi, double prenosPodatkov)`, `setLte(bool lte)`, `getLte`, `setCenaKlicaMin(double cenaKlicaMin)`, `getCenaKlicaMin`, `setCenaSms(double cenaSms)`, `getCenaSms`, `setCenaPrenosMb(double cenaPrenosMb)`, `getCenaPrenosMb`, `dodajKlicMin(double klicMin)`, `dodajSms(int sms)`, `dodajPrenosMb(double prenosMb)`, `getSkupnaCena`
- InternetniPaket: `InternetniPaket(String naziv, double narocnina, bool iptv, bool stacionarniTelefon)`, `InternetniPaket(String naziv, double narocnina, bool iptv, bool stacionarniTelefon, MobilniPaket mobilniPaket)`, `imaIptv`, `setIptvShema(String iptvShema)`, `getIptvShema`, `imaStacionarniTelefon`, `setStacionarnaStevilka(String stacionarnaStevilka)`, `getStacionarnaStevilka` `imaMobilniPaket`, `getMobilniPaketNaziv`

Drugi nivo implementirajte s poljubnimi podatki in morebitnim pripadajočim vedenjem za dva operaterja. V paketu ustvarite vstopno točko, ki bo vključevala nekaj primerov iz prvega in drugega nivoja ter uporabljala implementirano vedenje. Glede na izvedbo operacij v programu dodajte ustrezen izpis.

## Naloga 8 (pretvorbe)

Napišite razrede za hirerarhijo dedovanja oseb v okviru šole - dijak, profesor, ravnatelj. Vsem naj bo skupno, da jih prepoznamo po imenu in priimku ter naslovu bivanja. Preko vedenja omenjene podatke lahko pridobimo, naslov pa jim smemo spremeniti tudi kasneje. Njihove podrobnosti lahko izpišemo z metodo `toString`. Vsaki izmed navedenih entitet dodajte še specifično vedenje:

- Dijak: `Dijak(String imePriimek, String naslov, int razred, String oznakaRazreda)`, `dodajOceno(String predmet, int ocena)`, `izpisiOcene`, `getPovprecjeOcen`
- Profesor: `Profesor(String imePriimek, String naslov, String[] poucujePredmete)`, `Profesor(ime Priimek, String naslov, String[] poucujePredmete, String razrednikRazreda)`, `izpisiPredmete`, `getSteviloPredmetov`, `jeRazrednik`, `predstaviRazred(Dijak[] dijaki)`
- Ravnatelj: `Ravnatelj(String imePriimek, String naslov, String datumNastopa, String datumZakljucka)`, `Ravnatelj(String imePriimek, String naslov, String datumNastopa, String datumZakljucka, String[] poucujePredmete)`, `getDatumNastopa`, `getDatumZakljucka`, `sePoucuje`, `izpisiPredmete`, `getSteviloPredmetov`

Ustvarite ustrezne razrede ter implementirajte zahtevano vedenje. V paket dodajte vstopno točko, ki vključuje eno skupno tabelo z različnimi objekti ustvarjenih razredov, nato pa v zanki uporabite vse funkcionalnosti, ki so specifične zanje in pripravite poljuben izpis vseh njihovih podatkov.

## Naloga 9 (abstraktni razredi in metode)

Ustvarite hierarhijo dedovanja likov za krog, pravokotnik, kvadrat in enakostranični trikotnik. Vsak izmed njih ima lahko določeno barvo ter možnost celotnega barvanja ali samo robov. Oba podatka smemo pridobiti ali nastaviti tudi kasneje na posameznem objektu. Poleg tega mora imeti vsak lik določeno vedenje za pridobivanje obsega in ploščine ter možnost izpisa njegovega stanja s pomočjo metode `toString` - v kolikor lik razširja obstoječega, naj bo vključeno tudi stanje starševskega lika. Dodatno vedenje naj bo specifično še za posamezen lik:

- Krog: `Krog(double polmer)`, `Krog(double polmer, String barva, boolean obarvan)`, `getPolmer`, `setPolmer(double polmer)`
- Pravokotnik: `Pravokotnik(double dolzina, double sirina)`, `Pravokotnik(double dolzina, double sirina, String barva, boolean obarvan)`, `getDolzina`, `setDolzina(double dolzina)`, `getSirina`, `setSirina(double sirina)`
- Kvadrat: `Kvadrat(double stranica)`, `Kvadrat(double stranica, String barva, boolean obarvan)`, `getStranica`, `setStranica(double stranica)`, `setDolzina(double stranica)`, `setSirina(double stranica)`
- Trikotnik: `Trikotnik(double stranica)`, `Trikotnik(double stranica, String barva, boolean obarvan)`, `getStranica`, `setStranica(double stranica)`

Implementirajte vse zahtevane operacije in v paket dodajte še vstopno točko, ki vključuje tabelo vseh likov ter uporablja vsem skupno in specifično vedenje posameznega lika. Pri uporabi si pomagajte z izpisom njihovih podatkov.

## Naloga 10 (abstraktni razredi in metode)

Napišite programske gradnike za hierarhijo dedovanja divjih (tiger, opica, medved) in domačih živali (pes, mačka, kunec). Veriga dedovanja do zadnjega razreda naj bo dolga vsaj dva nivoja, pri čemer upoštevamo, da lahko ustvarimo le objekte dejanskih živali. Skupno vedenje vseh živali naj bo določeno z metodo `getVrsta` in `getIme`. Vrsta definira tip živali v katero jo uvrščamo, ime pa lahko podamo le pri domačih živalih, medtem ko naj divje vračajo generično ime - naziv živali. Domače živali morajo vsebovati dodatni skupni metodi:

- `pozdravi`, ki vrača niz po katerem prepoznamo žival
- `pozdravi(...)`, ki sprejme drugo domačo žival in izpiše niz v obliki npr. `Pes Floki [pozdravlja] kunec Pepi`, pri čemer `[pozdravlja]` nadomestite z nizom, ki ga vrača prejšnja metoda brez parametra

Ustvarite ustrezne razrede, napišite konstruktorje, ki ustrezajo zahtevam in implementirajte opisane metode. V paket dodajte vstopno točko, ki vsebuje objekte vseh ustvarjenih razredov in izpisuje njihove podatke. Za domače živali naredite še nekaj klicev metode `pozdravi` med različnimi objekti.
