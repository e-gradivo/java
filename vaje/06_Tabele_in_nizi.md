# Tabele in nizi

Namig: Pri reševanju nalog posušajte uporabiti raznolike metode razreda String, kot so `contains`, `format`, `split`, `toLowerCase`.

## Naloga 1

Napišite program, ki inicializira tabele, nato pa ročno nastavi vrednosti s pomočjo indeksov:

- `celaStevila` z velikostjo 3 in vrednostmi `1, 2, 3`
- `besede` z velikostjo 2 in vrednostma `hello, world`
- `crke` z velikostjo 4 in vrednostmi `a, b, c, d`

Na koncu izpiši število elementov posamezne tabele.

Izhod:

```text
celaStevila: 3
besede: 2
crke: 4
```

Rešitev:

<details>
<summary>Naloga1.java</summary>

```java
class Naloga1 {
    public static void main(String[] args) {
        int[] celaStevila = new int[3];
        celaStevila[0] = 1;
        celaStevila[1] = 2;
        celaStevila[2] = 3;

        String[] besede = new String[] { "hello", "world" };

        char[] crke = { 'a', 'b', 'c', 'd' };

        System.out.println("celaStevila: " + celaStevila.length);
        System.out.println("besede: " + besede.length);
        System.out.println("crke: " + crke.length);
    }
}
```

</details>

## Naloga 2

Napišite program, ki inicializira naslednje tabele:

- `celaStevila` z vrednostmi `10, 20, 30, 40, 50`
- `besede` z vrednostmi `vceraj, danes, jutri`
- `crke` z vrednostmi `x, y, z, w`

Na koncu naj za vsako izpiše število elementov posamezne tabele.

Izhod:

```text
celaStevila: 5
besede: 3
crke: 4
```

Rešitev:

<details>
<summary>Naloga2.java</summary>

```java
class Naloga2 {
    public static void main(String[] args) {
        int[] celaStevila = new int[5];
        celaStevila[0] = 10;
        celaStevila[1] = 20;
        celaStevila[2] = 30;
        celaStevila[3] = 40;
        celaStevila[4] = 50;

        String[] besede = new String[] { "vceraj", "danes", "jutri" };

        char[] crke = { 'x', 'y', 'z', 'w' };

        System.out.println("celaStevila: " + celaStevila.length);
        System.out.println("besede: " + besede.length);
        System.out.println("crke: " + crke.length);
    }
}
```

</details>

## Naloga 3

S pomočjo tabel sestavite program za izris kvadrata velikosti podane na vhodu, ki ne sme biti manjša od 3.

Vhod:

```text
4
```

Izhod:

```text
- - - -
- - - -
- - - -
- - - -
```

Rešitev:

<details>
<summary>Naloga3.java</summary>

```java
import java.util.Scanner;

class Naloga3 {
    public static void main(String[] args) {
        System.out.print("Velikost kvadrata: ");
        Scanner scn = new Scanner(System.in);
        int velikost = scn.nextInt();

        if (velikost < 3) {
            System.out.println("Velikost kvadrata je manjša od 3.");
        } else {
            int[][] kvadrat = new int[velikost][velikost];
            for (int i = 0; i < kvadrat.length; i++) {
                for (int j = 0; j < kvadrat[i].length; j++) {
                    System.out.print("- ");
                }
                System.out.println();
            }
        }
    }
}
```

</details>

## Naloga 4

Predhodno nalogo nadgradite z možnostjo izrisa pravokotnika, kjer dolžina oz. širina stranice prav tako ne sme biti manjša od 3.

Vhod:

```text
pravokotnik
4x3
```

Izhod:

```text
- - - -
- - - -
- - - -
```

Rešitev:

<details>
<summary>Naloga4.java</summary>

```java
import java.util.Scanner;

class Naloga4 {
    public static void main(String[] args) {
        Scanner scn = new Scanner(System.in);
        System.out.print("Kvadrat/pravokotnik: ");
        String tip = scn.nextLine();

        System.out.print("Velikost: ");
        String velikost = scn.nextLine();
        scn.close();

        int a = 0;
        int b = 0;

        if (tip.equalsIgnoreCase("kvadrat")) {
            a = b = Integer.parseInt(velikost);
        } else if (tip.equalsIgnoreCase("pravokotnik")) {
            String[] velikosti = velikost.split("x");
            a = Integer.parseInt(velikosti[0]);
            b = Integer.parseInt(velikosti[1]);
        }

        if (a < 3 || b < 3) {
            System.out.printf("Velikost %sa je manjša od 3.\n", tip);
        } else {
            int[][] kvadrat = new int[a][b];
            for (int i = 0; i < kvadrat.length; i++) {
                for (int j = 0; j < kvadrat[i].length; j++) {
                    System.out.print("- ");
                }
                System.out.println();
            }
        }
    }
}
```

</details>

## Naloga 5

Napišite program, ki uporabnika najprej vpraša po podatkovnem tipu `char` ali `int`. Glede na njegov vhod zgenerirajte 5 naključnih znakov oziroma števil in mu omogočite, da desetkrat ugiba, če je vnešena vrednost v tabeli. Glede na vsebovanost vrednosti izpišite stanje (uspeh ali neuspeh) in na koncu izpišite koliko elementov je uspel ugotoviti ter kateri so bili vsi elementi v tabeli. V primeru, da uporabnik ugotovi vse vrednosti predčasno, prekinite možnost dodatnih poskusov.

Vhod:

```text
int
0
1
2
3
4
5
6
7
8
9
```

Izhod:

```text
Izbrano ugotavljanje števil.
0 ni v tabeli.
1 ni v tabeli.
2 ni v tabeli.
3 ni v tabeli.
4 je v tabeli.
5 je v tabeli.
6 ni v tabelo.
7 je v tabeli.
8 ni v tabeli.
9 ni v tabeli.
--------------
Ugotovljenih 3/5.
Preostale vrednosti:
15
21
```

Rešitev:

<details>
<summary>Naloga5.java</summary>

```java
import java.util.Random;
import java.util.Scanner;

class Naloga5 {
    public static void main(String[] args) {
        Scanner scn = new Scanner(System.in);
        System.out.print("int/char: ");
        String tip = scn.nextLine();

        int velikost = 5;
        int steviloPoskusov = 10;
        boolean[] ugotovljeni = new boolean[velikost];
        int ugotovljenih = 0;
        Random rand = new Random();

        if (tip.equals("int")) {
            System.out.println("Izbrano ugotavljanje števil.");

            int[] nakljInt = new int[velikost];
            for (int i = 0; i < nakljInt.length; i++) {
                nakljInt[i] = rand.nextInt(10);
            }

            for (int i = 0; i < steviloPoskusov; i++) {
                System.out.print((i + 1) + ". poskus: ");
                int poskus = scn.nextInt();

                boolean ugotovljeno = false;
                for (int j = 0; j < nakljInt.length; j++) {
                    if (!ugotovljeni[j] && nakljInt[j] == poskus) {
                        ugotovljeni[j] = true;
                        ugotovljeno = true;
                        ugotovljenih++;
                        break;
                    }
                }

                if (ugotovljeno) {
                    System.out.println(poskus + " je v tabeli.");
                } else {
                    System.out.println(poskus + " ni v tabeli.");
                }
            }

            System.out.println("Ugotovljenih " + ugotovljenih + "/" + velikost);
            System.out.println("Preostale vrednosti:");
            for (int i = 0; i < nakljInt.length; i++) {
                if (!ugotovljeni[i]) {
                    System.out.println(nakljInt[i]);
                }
            }
        } else if (tip.equals("char")) {
            System.out.println("Izbrano ugotavljanje znakov.");

            char[] nakljChar = new char[velikost];
            for (int i = 0; i < nakljChar.length; i++) {
                nakljChar[i] = (char) (97 + rand.nextInt(25));
            }

            for (int i = 0; i < steviloPoskusov; i++) {
                System.out.print((i + 1) + ". poskus: ");
                String poskusStr = scn.nextLine();
                char poskus = poskusStr.charAt(0);

                boolean ugotovljeno = false;
                for (int j = 0; j < nakljChar.length; j++) {
                    if (!ugotovljeni[j] && nakljChar[j] == poskus) {
                        ugotovljeni[j] = true;
                        ugotovljeno = true;
                        ugotovljenih++;
                        break;
                    }
                }

                if (ugotovljeno) {
                    System.out.println(poskus + " je v tabeli.");
                } else {
                    System.out.println(poskus + " ni v tabeli.");
                }
            }

            System.out.println("Ugotovljenih " + ugotovljenih + "/" + velikost);
            System.out.println("Preostale vrednosti:");
            for (int i = 0; i < nakljChar.length; i++) {
                if (!ugotovljeni[i]) {
                    System.out.println(nakljChar[i]);
                }
            }
        } else {
            System.out.println("Ne podpiram podanega tipa?");
        }
        scn.close();
    }
}
```

</details>

## Naloga 6

Vojaki bi se na poziv _»V vrsto zbor!«_ morali razvrstiti po višini od najmanjšega do največjega, a tega ne znajo najbolje. Desetarja zanima, kdo je vsaj lokalno postavljen pravilno; ostale bo namreč kaznoval z dodatnimi sklecami. Vojak je postavljen lokalno pravilno, če je njegov levi sosed (če obstaja) nižji ali enako visok, desni sosed (če obstaja) pa višji ali enako visok kot on.

Napišite program, ki prebere zaporedje višin vojakov v »vrsti zbor« in izpiše indekse vseh
vojakov, ki so postavljeni lokalno pravilno. Če to ne velja za nikogar, naj program izpiše
NOBEDEN.

Vhod:

```text
10
185 172 180 181 190 183 178 185 191 207
```

Izhod:

```text
2
3
7
8
9
```

Rešitev:

<details>
<summary>Naloga6.java</summary>

```java
import java.util.Scanner;

class Naloga6 {
    public static void main(String[] args) {
        Scanner scn = new Scanner(System.in);
        System.out.print("Število elementov: ");
        String steviloElementovStr = scn.nextLine();
        int steviloElementov = Integer.parseInt(steviloElementovStr);

        System.out.print("Elementi: ");
        String elementiStr = scn.nextLine();
        String[] elementiPosamezno = elementiStr.split(" ");
        int[] elementi = new int[steviloElementov];
        for (int i = 0; i < elementiPosamezno.length; i++) {
            elementi[i] = Integer.parseInt(elementiPosamezno[i]);
        }

        boolean katerikoli = false;
        for (int i = 0; i < elementi.length; i++) {
            boolean pravilno = ((i == 0) || (i > 0 && elementi[i - 1] < elementi[i]))
                    && ((i == elementi.length - 1) || (i < elementi.length - 1 && elementi[i + 1] > elementi[i]));
            if (pravilno) {
                katerikoli = true;
                System.out.println(i);
            }
        }

        if (!katerikoli) {
            System.out.println("NOBEDEN");
        }

        scn.close();
    }
}
```

</details>

## Naloga 7

Športniki tekmujejo na teku na 60m z ovirami. Zaradi potreb naše naloge so spremenili pravila in imajo odslej na voljo dva poskusa, čas pa se meri le s celimi sekundami. Najmanjša vsota časa obeh poskusov da zmagovalca.

Sestavite program, ki bo na vhodu najprej sprejel število tekmovalcev ter shranil njihova imena. Nato naj se za posamezno ime izpiše možnost vnosa rezultatov obeh krogov. Na koncu naj se rezultati izpišejo v vrstnem redu od najhitrejšega (zmagovalca) navzdol z ustreznimi končnimi uvrstitvami.

Vhod:

```text
2
Alice Ableton
Bob Bradley
15
16
14
12
```

Izhod:

```text
Število tekmovalcev: 2
----------------------
Rezultati:
1.  Bob Bradley  (1p: 14s, 2p: 12s)  ...  26s
2.  Alice Ableton  (1p: 15s, 2p: 16s) ...  31s
```

Rešitev:

<details>
<summary>Naloga7.java</summary>

```java
import java.util.Scanner;

class Naloga7 {
    public static void main(String[] args) {
        Scanner scn = new Scanner(System.in);
        System.out.print("Število tekmovalcev: ");
        String steviloTekmovalcevStr = scn.nextLine();
        int steviloTekmovalcev = Integer.parseInt(steviloTekmovalcevStr);

        String[] tekmovalci = new String[steviloTekmovalcev];
        for (int i = 0; i < steviloTekmovalcev; i++) {
            System.out.print("Ime tekmovalca " + (i + 1) + ".: ");
            tekmovalci[i] = scn.nextLine();
        }

        int steviloPoskusov = 2;
        int[][] rezultati = new int[steviloTekmovalcev][steviloPoskusov];
        for (int i = 0; i < steviloTekmovalcev; i++) {
            for (int j = 0; j < steviloPoskusov; j++) {
                System.out.print("Rezultat " + (j + 1) + ". poskusa za tekmovalca " + tekmovalci[i] + ": ");
                rezultati[i][j] = Integer.parseInt(scn.nextLine());
            }
        }

        // Seštevek časov
        int[] zdruzeniRezultati = new int[steviloTekmovalcev];
        for (int i = 0; i < zdruzeniRezultati.length; i++) {
            int skupaj = 0;
            for (int j = 0; j < rezultati[i].length; j++) {
                skupaj += rezultati[i][j];
            }
            zdruzeniRezultati[i] = skupaj;
        }

        // Shranimo prvotne indekse tekmovalcev
        int[] zdruzeniVrstniRed = new int[zdruzeniRezultati.length];
        for (int i = 0; i < zdruzeniVrstniRed.length; i++) {
            zdruzeniVrstniRed[i] = i;
        }

        // Uporabimo mehurčno urejanje za pridobivanje pravilnega vrstnega reda
        for (int i = 0; i < zdruzeniRezultati.length; i++) {
            for (int j = 1; j < (zdruzeniRezultati.length - i); j++) {
                if (zdruzeniRezultati[j - 1] > zdruzeniRezultati[j]) {
                    int rez = zdruzeniRezultati[j - 1];
                    zdruzeniRezultati[j - 1] = zdruzeniRezultati[j];
                    zdruzeniRezultati[j] = rez;

                    int red = zdruzeniVrstniRed[j - 1];
                    zdruzeniVrstniRed[j - 1] = zdruzeniVrstniRed[j];
                    zdruzeniVrstniRed[j] = red;
                }
            }
        }

        System.out.println("\nŠtevilo tekmovalcev: " + steviloTekmovalcev + "\n----------------------\nRezultati:");
        for (int i = 0; i < zdruzeniVrstniRed.length; i++) {
            int idx = zdruzeniVrstniRed[i];
            System.out.printf("%d. %s (1p: %ds, 2p: %ds) ... %ds\n", (i + 1), tekmovalci[idx], rezultati[idx][0],
                    rezultati[idx][1], zdruzeniRezultati[i]);
        }

        scn.close();
    }
}
```

</details>

## Naloga 8

Napišite poenostavljeno različico programa `sed`, ki podpira samo zamenjavo besedila. Kot prvi argument programa podprite dve stikali:

- `g`: globalna zamenjava niza (zamenjamo vse pojavitve prvotnega niza); privzeto naj se sicer zamenja samo prva pojavitev niza.
- `i`: upoštevamo iskanje po malih in velikih znakih (ang. _case insensitive_); privzeto naj se zamenja samo nize, ki so napisani v izvorni velikosti črk.

Uporabnik naj najprej vnese niz, ki ga želi zamenjati, nato niz za zamenjavo in na koncu še celotno besedilo.

Vhod:

```text
// Aplikacijo zaženemo kot:
// java naloga8 gi

svet
program
Pozdravljen, svet! Svet, pozdravljen.
```

Izhod:

```text
Pozdravljen, program! program, pozdravljen.
```

Rešitev:

<details>
<summary>Naloga8.java</summary>

```java
import java.util.Scanner;
import java.util.regex.Pattern;

class Naloga8 {
    public static void main(String[] args) {
        boolean g = false;
        boolean i = false;
        if (args.length > 0) {
            String arg = args[0];
            g = arg.contains("g");
            i = arg.contains("i");
        }

        Scanner scn = new Scanner(System.in);

        System.out.print("Išči: ");
        String isci = scn.nextLine();

        System.out.print("Zamenjaj z: ");
        String zamenjaj = scn.nextLine();

        System.out.print("Vhodno besedilo: ");
        String besedilo = scn.nextLine();

        String moznosti = i ? "(?i)" : "";
        String rezultat = "";
        if (g) {
            rezultat = besedilo.replaceAll(moznosti + Pattern.quote(isci), zamenjaj);
        } else {
            rezultat = besedilo.replaceFirst(moznosti + Pattern.quote(isci), zamenjaj);
        }
        System.out.println(rezultat);

        scn.close();
    }
}
```

</details>

## Naloga 9

Sestavite program za štetje besed in izpis pogostosti pojavitve, ki služi kot osnova za algoritem TF.IDF (uporablja se v okviru strojnega učenja). Zajeti je potrebno vse besede, ki se pojavijo v besedilu in prešteti kolikokrat se pojavijo. Odstranite tudi vsa najpogostejša ločila (pika, vejica, dvopičje, podpičje, klicaj, pomišljaj, ...). Na koncu naj program izpiše seznam besed (naj bodo zapisane z malimi črkami) in število pojavitev v besedilu.

Vhod:

```text
Pozdravljen, svet! Program, pozdravljen.
```

Izhod:

```text
pozdravljen (2)
svet (1)
program (1)
```

Rešitev:

<details>
<summary>Naloga9.java</summary>

```java
import java.util.Scanner;

class Naloga9 {
    public static void main(String[] args) {
        Scanner scn = new Scanner(System.in);

        System.out.print("Vhodno besedilo: ");
        String besedilo = scn.nextLine();
        scn.close();

        String[] besede = besedilo.split(" ");
        for (int i = 0; i < besede.length; i++) {
            besede[i] = besede[i].replace(".", "").replace(",", "").replace(":", "").replace(";", "").replace("!", "")
                    .replace("-", "").toLowerCase();
        }

        int[] stevec = new int[besede.length];
        boolean[] preskoci = new boolean[besede.length];
        for (int i = 0; i < besede.length; i++) {
            for (int j = i + 1; j < besede.length; j++) {
                if (!preskoci[j] && besede[i].equals(besede[j])) {
                    stevec[i]++;
                    preskoci[j] = true;
                }
            }
        }

        for (int i = 0; i < besede.length; i++) {
            if (!preskoci[i]) {
                System.out.printf("%s (%d)\n", besede[i], (stevec[i] + 1));
            }
        }
    }
}
```

</details>
