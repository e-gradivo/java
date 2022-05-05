# Vhod in izhod

## Naloga 1

Napiši program, ki bo na vhodu sprejel dva ali štiri argumente. V primeru dveh:

1. način delovanja programa
2. pot do datoteke za obdelavo

V primeru štirih:

1. način delovanja programa
2. število vrstic za preskok
3. število vrstic za branje
4. pot do datoteke za obdelavo

Načina delovanja programa sta:

- `glava`: beremo datoteko od začetka (od prve vrstice proti zadnji)
- `rep`: beremo datoteko od konca (od zadnje vrstice proti prvi)

Kadar nimamo podanih podatkov za število vrstic velja naslednje:

- privzeto število vrstic za preskok je `0`
- privzeto število vrstic za branje je `10`

Prebrane vrstice naj se izpisujejo na standardni izhod. Ustvari ustrezne pakete in loči kodo po njeni kontekstualni funkcionalnosti. Vstopna točka programa naj vsebuje zgolj branje in obdelavo argumentov, vso ostalo logiko pa naj posreduje naprej razredom, ki bodo znali sprocesirati ukaz do konca. V primeru neustreznih vhodnih podatkov naj program izpiše podrobno sporočilo o napaki (npr. vhodni podatki niso ustrezni / datoteka ne obstaja / datoteka nima ustreznega števila vrstic).

## Naloga 2

Ustvarite program, ki bo na vhodu sprejel tri argumente:

1. velikost črk - možnosti: V (velike) / M (male) / N (nespremenjeno)
2. pot do vhodne datoteke
3. pot do izhodne datoteke

Ključna naloga programa je, da vsebino iz vhodne datoteke obrne, na primer spremeni iz `Dober dan!` v `!nad reboD` in zapiše v izhodno datoteko. Glede na prvi argument naj upošteva tudi spremembo velikosti črk, za prejšnji primer bi to bilo:

- V: `!NAD REBOD`
- M: `!nad rebod`
- N: `!nad reboD`

V primeru uporabe izhodne datoteke kot vhodne po prvi izvedbi programa, se mora besedilo pravilno obrniti v izvorno obliko. Ustvari ustrezne pakete in loči kodo po njeni kontekstualni funkcionalnosti. Vstopna točka programa naj vsebuje zgolj branje in obdelavo argumentov, vso ostalo logiko pa naj posreduje naprej razredom, ki bodo znali sprocesirati ukaz do konca. V primeru neustreznih vhodnih podatkov naj program izpiše podrobno sporočilo o napaki (npr. vhodni podatki niso ustrezni / datoteka ne obstaja / datoteka nima ustreznega števila vrstic).
