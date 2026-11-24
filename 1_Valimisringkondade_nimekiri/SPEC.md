# 1 Valimisringkondade nimekiri

## Protseduur

VIS3 edastab EHS-le teabe valimisringkondade kohta.

Andmed edastatakse inim-masin-protseduuriga:

1) VIS peakasutaja koostab VIS3-s valimisringkondade nimekirja ja allkirjastab selle VIS3-s digitaalselt (ID-kaardi, Mobiil-ID või Smart-ID-ga). Iga allkirjastamine loob uue digikonteineri;

2) VIS peakasutaja laeb allkirjastatud digikonteineri VIS3-st alla ja annab selle EHS operaatorile;

3) EHS operaator laeb digikonteineri EHS-i.

Edastatav fail on ASiC-E digikonteiner (`.asice`), mis sisaldab üht JSON-formaadis andmefaili.

Andmefaili struktuur on kirjeldatud JSON schema-ga. Kirjeldus on kooskõlastatud EHS omanikuga.

EHS senine liides VIS2-ga on spetsifitseeritud dokumendis "IVXV protokollide kirjeldus" (v 1.5.0, IVXV-PR-1.5.0, 20.04.2019), [https://www.valimised.ee/sites/default/files/uploads/eh/IVXV-protokollid.pdf](https://www.valimised.ee/sites/default/files/uploads/eh/IVXV-protokollid.pdf), jaotises 3.2 "Valimisjaoskondade ja -ringkondade nimekiri".

Valimistel, kus saavad osaleda alaliselt välisriigis elavad valijad kantakse nad valijate nimekirja tunnusega `FOREIGN`. Sellisel juhul peab valimisringkondade nimekiri sisaldama regiooni nende valijate jaoks ning iga ringkond peab sisaldama eraldi jaoskonda, kus nende häälte üle arvestust peetakse. Nii selle regiooni kui jaoskondade tunnuseks on fiktiivne EHAK: `0000`. Näitefailis [districts_RK.json](districts_RK.json) on näha nii regiooni korrektne lisamine kui ka välishääletajate jaoskonna korrektne lisamine igasse ringkonda.



## Edastatav fail

Valimissündmuse identifikaator peab vastama formaadile [Valimissündmuse identifikaator](../valimissündmuse_identifikaator.md).

Andmefaili struktuur (JSON-skeem): [districts.schema](districts.schema)

### Faili nimi

Digikonteineri nimi on kujul `<valimissündmuse identifikaator>_ELECTORAL_DISTRICTS_<nr>.asice`, kus `<nr>` on valimissündmuse valimisringkondade nimekirja ekspordi järjenumber. Järjenumber algab nullist ja suureneb iga uue allkirjastatud ekspordiga ühe võrra. Suurima järjenumbriga konteiner on kõige värskem.

Konteineris olev andmefail on sama nimega, kuid laiendiga `.json`.

### Näited

Allkirjastatud digikonteinerid (ASiC-E):

- [EP_2026_ELECTION_RESULTS_ELECTORAL_DISTRICTS_1.asice](EP_2026_ELECTION_RESULTS_ELECTORAL_DISTRICTS_1.asice)
- [KOV_2026_ELECTION_RESULTS_ELECTORAL_DISTRICTS_0.asice](KOV_2026_ELECTION_RESULTS_ELECTORAL_DISTRICTS_0.asice)
- [RH_2026_ELECTION_RESULTS_ELECTORAL_DISTRICTS_0.asice](RH_2026_ELECTION_RESULTS_ELECTORAL_DISTRICTS_0.asice)
- [RK_2026_ELECTION_RESULTS_ELECTORAL_DISTRICTS_1.asice](RK_2026_ELECTION_RESULTS_ELECTORAL_DISTRICTS_1.asice)

Andmefailid (JSON):

- [district_KOV.json](district_KOV.json)
- [districts_EP.json](districts_EP.json)
- [districts_RH.json](districts_RH.json)
- [districts_RK.json](districts_RK.json)

## Taustainfo

Kandidaate on võimalik valimisele üles seada ainult konkreetses valimisringkonnas. Ringkondade järgi antakse valijatele hääletamise valikud:

1. Iga valija kuulub talle määratud valimisringkonda;
2. Kõigis ühe ringkonna jaoskondades saavad valijad teha valiku vaid selle ringkonna valikute vahel;

Eesti riiklikel valimistel eristatakse kohalike omavalitsuste volikogude (KOV) valimisi, Riigikogu valimisi, Euroopa Parlamendi valimisi ning rahvahääletusi.

KOV valimised korraldatakse vastavalt seadusele „Kohaliku omavalitsuse volikogu valimise seadus“. Valimine toimub kohaliku omavalitsuse tasandil, igal omavalitsusel on oma hääletamistulemus. Valimisringkonnad moodustatakse omavalitsuse tasemel vastavalt seaduses kirjeldatud reeglitele.

Riigikogu valimised korraldatakse vastavalt seadusele „Riigikogu valimise seadus“. Valimine toimub riigi tasandil. Riik jaguneb 12 valimisringkonnaks. Hääletamistulemus tehakse kindlaks iga valimisringkonna kohta.

Europarlamendi valimised korraldatakse vastavalt seadusele „Euroopa Parlamendi valimise seadus“. Valimine toimub riigi tasandil, hääletamistulemus on kõigile kohalikele omavalitsustele ühine. Terve riik on üks valimisringkond.

Rahvahääletused korraldatakse vastavalt seadusele „Rahvahääletuse seadus“. Valimine toimub riigi tasandil, hääletamistulemus on kõigile kohalikele omavalitsustele ühine. Terve riik on üks valimisringkond.

Erinevad valimised ei erine elektroonilise hääletamise andmevormingute ja protseduuride poolest. Erinevad ringkondade jaotused hallatakse VIS3 poolt.

Kandidaate on võimalik valimisele üles seada ainult konkreetses valimisringkonnas. Valijad on jaotatud valimisringkondade vahel. Valija saab teha valiku ainult tema ringkonnas kandideerivate kandidaatide vahel.

Kuna kohaliku omavalitsuse volikogude valimisel toimub valimine Eesti omavalitsuste (vallad, linnad) tasemel, siis kasutatakse elektroonilise hääletamise protokollistikus valimisringkondade kirjeldamisel ning valijate ja valikute ringkonnakuuluvuse näitamisel Eesti haldus- ja asustusjaotuse klassifikaatorit EHAK

Näiteks:
• Tallinna linna Pirita linnaosa EHAK kood on 0596;
• Anija valla EHAK kood on 0141.

Riigi tasemel toimuvatel valimistel pannakse ringkonna EHAK koodiks kokkuleppeliselt 0.

Riigikogu ja europarlamendi valimistel ning rahvahääletusel moodustatakse nimekirjas igasse ringkonda fiktiivne üksus alaliselt välisriigis elavate valijate tarbeks. Selle üksuse number on 0 ning vastav EHAK kood on 0000.
