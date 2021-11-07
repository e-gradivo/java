# Objektno programiranje

## Naloga 1

Ustvarite razred `Pes` z lastnostmi `ime`, `pasma`, `starost`, `barva` in vedenjem `opis`, `lajaj`, `sedi`, `spi`. Po klicu metod naj se izpišejo lastnosti in naziv posameznega vedenja (npr. `Floki (pasma: shiba inu, starost: 5 let, barva: oranžna) laja!`).

## Naloga 2

Imamo avto z lastnostmi `znamka`, `model`, `cena`, `voznik` ter funkcionalnostmi `opis`, `nastaviVoznika`, `trenutniVoznik`, `izstopVoznika`, `vzgi`, `ugasni`, `premakni`. V avtomobilu mora biti za delovanje zadnjih treh funkcionalnosti voznik, v nasprotnem primeru naj se izpiše, da avto brez voznika ne deluje. Voznika predstavimo z imenom, številom let imetja vozniškega izpita in starostjo. Njegovo vedenje lahko predstavi s svojim opisom. Prav tako naj funkcionalnosti delujejo po logičnem zaporedju - v kolikor želimo zamenjati voznika, mora prejšnji izstopiti; avto se lahko premakne ali ugasne le če je vžgan; avto lahko vžge samo, če še ni. Ustvarite ustrezne razrede in implementirajte funkcionalnost.

## Naloga 3

Obstaja več različnih igralnih kock, na primer s 6, 12 in 20 ploskvami. Ustvarite razred, ki bo sprejel število ploskev in imel metode `vrednosti` (izpiše vse ploskve in število pik na njih), `metanje` (vrne naključno število pik glede na ploskve kocke), `zaporedje(int poskusov)` (vrne tabelo naključnih vrednosti števila pik v velikosti poskusov). Nato ustvarite objekte za vse tri omenjene igralne kocke in izpišite vrednosti po izvedbi vseh metod - uporabite tabele kamor shranite število ploskev kock in nato s pomočjo zanke (brez ponavljanja kode) dokončajte ustvarjanje in izpis.

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
