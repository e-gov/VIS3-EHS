# 1 Valimisringkondade nimekiri

## Protseduur

VIS3 edastab EHS-le teabe valimisringkondade kohta.

Andmed edastatakse inim-masin-protseduuriga:

1) VIS peakasutaja laeb JSON faili VIS3-st alla;

2) VIS peakasutaja allkirjastab faili digitaalselt väljaspool VIS-i ja annab selle EHS operaatorile;

3) EHS operaator laeb digiallkirjastatud faili EHS-i.

Fail on JSON-formaadis. Faili ei allkirjastata.

Faili struktuur on kirjeldatud JSON schema-ga. Kirjeldus on kooskõlastatud EHS omanikuga.

EHS senine liides VIS2-ga on spetsifitseeritud dokumendis "IVXV protokollide kirjeldus" (v 1.5.0, IVXV-PR-1.5.0, 20.04.2019), [https://www.valimised.ee/sites/default/files/uploads/eh/IVXV-protokollid.pdf](https://www.valimised.ee/sites/default/files/uploads/eh/IVXV-protokollid.pdf), jaotises 3.2 "Valimisjaoskondade ja -ringkondade nimekiri".

Valimistel, kus saavad osaleda alaliselt välisriigis elavad valijad kantakse nad valijate nimekirja tunnusega `FOREIGN`. Sellisel juhul peab valimisringkondade nimekiri sisaldama regiooni nende valijate jaoks ning iga ringkond peab sisaldama eraldi jaoskonda, kus nende häälte üle arvestust peetakse. Nii selle regiooni kui jaoskondade tunnuseks on fiktiivne EHAK: `0000`. Näitefailis [districts_RK.json](districts_RK.json) on näha nii regiooni korrektne lisamine kui ka välishääletajate jaoskonna korrektne lisamine igasse ringkonda.



## Edastatav fail

Valimissündmuse identifikaator peab vastama formaadile [Valimissündmuse identifikaator](../valimissündmuse_identifikaator.md).

Faili struktuur (JSON-skeem): [districts.schema](districts.schema)

Näited (JSON):

- [district_KOV.json](district_KOV.json)
- [districts_EP.json](districts_EP.json)
- [districts_RH.json](districts_RH.json)
- [districts_RK.json](districts_RK.json)

