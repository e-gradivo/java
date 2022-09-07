# Uvod v programiranje

Definicija [računalnika po SSKJ](https://www.fran.si/iskanje?FilteredDictionaryIds=130&View=1&Query=ra%C4%8Dunalnik) je naslednja:

> elektronska naprava za reševanje nalog na osnovi vloženega programa

Izbrana razlaga nam pove, da gre za elektronsko napravo, vendarle pa je prva povsem splošna:

> priprava za avtomatsko opravljanje računskih operacij

Iz obeh definicij lahko torej sklepamo, da je računalnik prvotno namenjen računanju ali obdelavi vhodnih podatkov z vnaprej pripravljenimi operacijami.

Za lažjo predstavitev se vrnimo na definicijo, ki omenja elektronsko napravo ter izpostavimo stacionarni in prenosni računalnik. Pod njunim pokrovom najdemo vezja z elektronskimi komponentami, ki jih v splošnem poimenujemo kar strojna oprema. Iz arhitekture računalništva vemo, da za veljavnost prve navedene definicije potrebujemo enoto, ki izvaja **operacije**, za izvedbo operacij pa potrebujemo **podatke**. Ti so lahko začasni ali trajni, temu primerna pa sta tudi sklopa arhitekture, ki omogočata branje in zapis.

Definicija iz katere smo izhajali vključuje še eno besedo, ki ji doslej nismo posvečali posebne pozornosti, saj jo v povezavi z računalnikom skoraj ne moremo spregledati. Računalnik nam torej omogoča reševanje nalog na osnovi vloženega **programa**. [Program po SSKJ](https://www.fran.si/iskanje?FilteredDictionaryIds=130&View=1&Query=program) bomo za naše potrebe definirali kot:

> urejen spisek instrukcij, ki določa vrsto in zaporedje operacij, potrebnih, da (elektronski) računalnik reši nalogo

Če se navežemo na računalniško arhitekturo, vemo da procesor podpira določen nabor instrukcij, s katerimi lahko izvajamo nadaljnje operacije. Zaporedju klicev teh instrukcij rečemo operacija in nam po njeni izvedbi običajno vrne nek rezultat, ki je posledica izvedbe uporabljenih instrukcij. Vse operacije, ki so del programa, moramo pred njihovim klicem definirati. To v osnovi storimo v času izdelave programa, temu postopku pa pravimo **programiranje**.

Operacije v programu izpolnjujejo zaporedje dejanj, ki jim običajno rečemo navodila. Za primer vzemimo naslednja:

- pozajtrkuj
- pojdi na avtobus
- zbudi se
- obuj si čevlje
- vstani

V kolikor sledimo njihovem zapisu, opazimo, da niso v pravem vrstnem redu. Situacijo lahko preslikamo neposredno na program na računalniku. Ugotovimo, da mora biti zaporedje dejanj in nadalje klicev operacij v pravem vrstnem redu, če želimo, da bo končni rezultat ustrezal našim pričakovanjem. Pri tem se navežimo na koren besede **račun***alnik*, saj si bomo operacijo najlažje predstavljali kot izračun nad dvemi številkami v okviru matematike.

Preden se podrobneje posvetimo opredeljevanju in lastnostim navodil v programih, moramo omeniti še, na kakšen način se sporazumevamo z računalnikom. Pri komuniciranju z ostalimi osebami uporabljamo naravni jezik, ki nam omogoča, da razumemo, kar nam nekdo pove in obratno. Podobno je tudi pri programiranju, kjer uporabljamo **programski jezik**, s katerim računalniku povemo, kaj točno od njega pričakujemo. Tako kot pri naravnih jezikih, obstajajo tudi različni programski jeziki. Obstajta dve kategoriji, v katere ju ločimo:

- splošno namenski programski jeziki *(ang. general-purpose programming language - GPL)*
- domensko specifični programski jeziki *(ang. domain-specific programming language - DSL)*

V nadaljevanju se bomo osredotočili na splošno namenske programske jezike, naš glavni cilj pa bo spoznati osnove programskega jezika Java.

## Algoritmi

Algoritem je končno zaporedje natančno določenih izvedljivih navodil, namenjenih reševanju problemske domene ali izvajanju izračuna. Podrobnost navodil je odvisna od končnega uporabnika in njegove stopnje razumevanja - v primeru ustreznega predznanja so navodila lahko zelo splošna, v nasprotnem primeru pa morajo biti zelo obsežna. Kot uporabnika lahko za začetek vzamemo človeka - strokovno podkovanemu bomo običajno dali osnovne smernice, medtem ko moramo laiku zagotoviti čimveč podrobnosti, da bo pravilno izvedel vse korake.

Kadar algoritem izvaja računalnik, gre za program, v katerem je zajet celoten postopek. Podobno, kot pri strokovnosti osebe iz prejšnjega primera, so navodila v programih lahko povsem splošna ali pa zelo obsežna. Odvisno od tega kakšno strojno in obstoječo programsko opremo uporabljamo za izvedbo lastnega programa.

Primer algoritma:

1. Zberemo in odmerimo sestavine
2. Zmešamo sestavine in zgnetemo v testo
3. Testo oblikoujemo v kepo, zavijemo v folijo in za eno uro postavimo v hladilnik
4. Segrejemo pečico na 200 stopinj Celzija
5. Testo na pomokani delovni površini razvaljamo na 5 mm in iz njega izrežemo zvezdice
...

Rezultat: Čokoladne zvezdice

Iz primera algoritma lahko razberemo, da zanj veljajo določene zakonitosti, ki jih moramo upoštevati, če želimo pridobiti ustrezen rezultat.

### Lastnosti

Če želimo navodila za izvedbo zaporedja dejanj označiti kot algoritem, morajo ta upoštevati ...

- popolnost - vsa dejanja algoritma morajo biti natančno definirana.
- nedvoumnost - množica instrukcij je nedvoumna le, če obstaja samo en način interpretacije ukazov.
- determinizem - sledenje instrukcijam bo vedno privedlo do želenega (enakega) končnega rezultata.
- končnost - izvajanje instrukcij se mora končati (po določenem številu korakov).

... poleg tega pa algoritem tudi:

- (lahko) sprejme podatke
- (običajno) vrne rezultat

### Želeni atributi

Ko zadostimo lastnostim algoritmov, se vprašamo kaj še lahko izboljšamo v navodilih, da bodo učinkovitejše opravljala svoje poslanstvo. Celoten postopek ponavadi želimo optimizirati tako, da vse korake izvedemo v najkrajšem možnem času, z najmanj porabljenimi viri. Hkrati naj bi bili vsi koraki enostavno razumljivi, da jih v primeru sprememb hitro prilagodimo. Rezultat algoritma mora biti enak ne glede na to ali upošteva omenjeno (je optimiziran, enostavno razumljiv) ali ne. Atributi, ki jih običajno želimo doseči so:

- splošnost - algoritem naj rešuje razred problemov, ne le enega. V primeru, da napišemo postopek za seštevanje števil, verjetno ne bomo pisali postopka za seštevanje števil 5 in 7, nato nov postopek za seštevanje drugih dveh števil in tako naprej. Postopek spišemo splošno, tako da lahko seštejemo poljubni dve števili.
- dobra struktura - algoritem je sestavljen iz blokov, ki jih je enostavno razložiti, so razumljivi in jih lahko preizkušamo ter spreminjamo. Bloki naj bi bili povezani tako, da jih lahko enostavno zamenjamo z drugimi (boljšimi/učinkovitejšimi) bloki.
- učinkovitost - algoritem naj bo hiter, majhen po obsegu in kompakten. Cilj pisanja postopka je, da je hiter, majhen in brez odvečnega izvajanja.
- enostavnost - algoritem naj bo razumljiv in enostaven za uporabo.
- robustnost - algoritem naj zajema vse robne primere, ki lahko nastopijo med njegovim izvajanjem. Cilj pisanja postopka je, da uspemo razrešiti tudi vmesne težave, ki se lahko pojavijo glede na okoljske spremembe.
- ekonomičnost - algoritem naj za svoje izvajanje porablja le toliko virov, kot je to zares potrebno. Cilj pisanja postopka je, da uporabimo najmanjše možno število virov ter ga s tem naredimo ekonomično sprejemljivega.

### Zapis

- naravni jezik - algoritem je izražen z besedami.
- grafično z diagramom poteka *(ang. flowchart)* - algoritem je predstavljen v obliki diagrama s simboli, povezanimi s puščicami v smeri poteka.
- psevdokoda - algoritem je predstavljen kot množica instrukcij, zapisanih v mešanici naravnega jezika in matematične notacije, ki so podobne tistim iz programskih jezikov.
- koda v izbranem programskem jeziku - algoritem je sestavljen iz instrukcij, ki so predpisane v dokumentaciji programskega jezika.

### Analiza

Pogosto se pojavi vprašanje koliko določenih virov je potrebno nameniti za izvedbo danega algoritma. Za pridobitev takšnih ocen so bile razvite metode za analizo algoritmov. Podrobneje se osredotočamo na:

- časovno zahtevnost
- prostorsko zahtevnost

Za zapis obeh ocen uporabimo **notacijo O**, s katero označimo odziv na spremembe glede na velikosti vhoda.
