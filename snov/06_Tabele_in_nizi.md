# Tabele in nizi

V tem poglavju spoznamo tabele in nize.

## Tabele

Tabela _(ang. array)_ je podatkovna struktura, ki hrani zbirko vrednosti istega podatkovnega tipa. Do posamezne vrednosti v zbirki dostopamo s pomočjo številčnega indeksa. Obstoječim tabelam ne moremo spremeniti velikosti.

```java
int[] a; // deklaracija
int a[]; // druga veljavna deklaracija
a = new int[] { 1, 2, 3, 4, 5 }; // inicializacija
a[0]; // dostop do vrednosti z indeksom 0
```

Ob inicializaciji tabele brez podanih specifičnih vrednosti elementov, imajo le-ti privzeto vrednost (`boolean => false`, `Object => null`, ...). Elementi so označeni s številskimi indeksi, ki se začnejo z 0. Torej do prvega elementa v tabeli dostopamo z 0, do drugega z 1 in tako naprej.

```java
// deklaracija
int[] a;
float[] b;
String[] c;

// inicializacija
int[] a = new int[100];
var b = new int[100];

int[] numbers = { 2, 3, 5, 7, 11, 13 };
String[] parts = {
    "Hello,",
    "world!",
    "World,",
    "hello!"
};

var nums = new int[] { 17, 19, 23, 29, 31, 37 };

// inicializacija prazne tabele
int[] x = new int[0];
var y = new int[] {};
```

Število elementov v tabeli je znano lastnosti `length` na objektu tabele. Za izpis vseh elementov si lahko pomagamo s klasično `for` zanko, obstaja pa posebna zanka `for each`, ki omogoča iteracijo po vrednostih tabele brez uporabe indeksov. Slednjo lahko uporabimo na vseh tipih zbirk, več o tem pa v poglavju objektnega programiranja.

```java
int[] numbers = { 1, 2, 3, 4, 5 };

// iteracija s klasično for zanko
for (int i = 0; i < numbers.length; i++) {
    System.out.println("Vrednost elementa z indeksom " + i + " je: " + numbers[i]);
}

// iteracija s for each zanko
for (int i : numbers) {
    System.out.println("Vrednost elementa: " + i);
}
```

Tabele lahko tudi kopiramo v poljubne druge spremenljivke, vendar moramo pri tem upoštevati, da gre pri tem le za referenciranje prvotne tabele in ne prenos vrednosti. To pomeni, da spreminjanje kopirane tabele rezultira v spremembe na prvotni in morebitnih ostalih kopiranih tabelah.

```java
String[] strings = new String[] { "a", "b", "c", "d" };
var stringsCopy = strings;
stringsCopy[0] = "z";
System.out.println(strings[0] + " == " + stringsCopy[0]);
```

Iz enostavnih tabel lahko sestavimo večdimenzionalne tabele, kjer namesto enega indeksa uporabljamo število indeksov, ki jih definira dimenzija tabele. Za dvodimenzionalno imamo tako 2 indeksa, za trodimenzionalno 3 in tako naprej.

```java
// deklaracija
double[][] balances; 
String[][] salutation;

// inicializacija
balances = new double[][] {
    {12.1, 15.4},
    {16.3, 45.2}
};
salutation = new String[][] {
    {"Mr.", "Mrs.", "Ms."},
    {"Alison", "Bradley", "Cooper"}
};

// iteracija
for (int i = 0; i < balances.length; i++) {
    System.out.print(i + ":  ");
    for (int j = 0; j < balances[i].length; j++) {
        System.out.print(balances[i][j] + "  ");
    }
    System.out.println();
}

for (int i = 0; i < salutation.length; i++) {
    for (int j = 0; j < salutation[i].length; j++) {
        if (i < salutation.length - 1 && j < salutation[i].length) {
            System.out.println(salutation[i][j] + " " + salutation[i + 1][j]);
        }
    }
}
```

Za konec podpoglavja še nekaj vprašanj:

- Kako skopiramo tabelo brez referenciranja (torej prenesemo vrednosti)?
- Kako povečamo tabelo, če želimo dodati element, ki presega deklarirano velikost?
- Kje bi lahko uporabili večdimenzionalne tabele in kako v tem primeru imenujemo indekse?

## Nizi

Tabelo znakov v Javi lahko zapišemo kot instanco razreda String. Nizi so konstante, kar pomeni, da njihove vrednosti ne moremo spremeniti po tem, ko so že ustvarjeni (so nespremenljivi oziroma ang. _immutable_).

```java
String newStr = "hello";
char[] newCharArray = new char[] { 'h', 'e', 'l', 'l', 'o' };
String strFromChar = new String(newCharArray); // ustvarimo niz iz tabele znakov

String helloStr = "Hello, world!"; // inicializacija
System.out.println(helloStr);
helloStr.substring(0, 5); // izrez prvih pet znakov - ne vpliva na niz, saj metoda vrne nov niz
System.out.println(helloStr); // nespremenjen niz po prejšnji operaciji
System.out.println(helloStr.substring(0, 5)); // niz po izrezu
```

Razred String vključuje številne metode za delo z nizi, podpira pa tudi operacijo s pomočjo operatorja za združevanje (konkatenacijo) `+`, ki omogoča lepljenje dveh nizov.

```java
String first = "Hello";
String second = "world";
String combined = first + ", " + second + "!";
System.out.println(combined);
```

Seznam nekaj najpogosteje uporabljenih metod:

- charAt
- compareTo
- concat
- contains
- endsWith
- equals
- format
- indexOf
- isBlank
- isEmpty
- join
- length
- replace
- replaceAll
- replaceFirst
- split
- startsWith
- toLowerCase
- toUpperCase
- trim

Za uporabo posameznih metod in zahtevanih argumentov preverimo [uradno dokumentacijo](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/lang/String.html).

Obstaja tudi dodaten razred StringBuffer, ki je za razliko od razreda String spremenljiv (ang. _mutable_) in omogoča vrivanje in dodajanje znakov na konec niza. Ima določeno kapaciteto (število znakov), ki jo v primeru prekoračitve pri izbrani operaciji samodejno poveča (realocira).

```java
StringBuffer sb = new StringBuffer();
StringBuffer sbAlloc = new StringBuffer(32); // nastavimo dolžino/kapaciteto niza
StringBuffer sbExisting = new StringBuffer("existing"); // nastavimo obstoječ niz
```

Glavni operaciji razreda sta `insert` in `append`, ki pod veljavnimi argumenti ustrezno spremenita niz.

```java
StringBuffer sb = new StringBuffer("world");
sb.insert(0, "Hello"); // vstavimo del niza na začetek
System.out.println(sb);
sb.insert(5, ", "); // vstavimo del niza z določenim odmikom
System.out.println(sb);
System.out.println(sb.append('!')); // klic metode spremeni objekt in hkrati vrne njegovo novo vrednost
System.out.println(sb); // preverimo, če je bil objekt s prejšnjo vrstico zares spremenjen
```

Razred StringBuffer podpira uporabo znotraj več niti (ang. _threads_) in posledično na določenih metodah izvaja sinhronizacijo. Kadar ne potrebujemo tovrstne podpore, raje uporabimo razred StringBuilder, saj je kompatibilen z razredom StringBuffer in v večini implementacij hitrejši.

```java
StringBuilder sb = new StringBuilder("world");
sb.insert(0, "Hello");
System.out.println(sb);
sb.insert(5, ", ");
System.out.println(sb);
System.out.println(sb.append('!'));
System.out.println(sb);
```
