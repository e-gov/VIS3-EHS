# 5 Tühistus- ja ennistusnimekiri

VIS3 edastab EHS-le tühistus- ja ennistusnimekirja (lühidalt - tühistusnimekiri).

Tühistusnimekiri sisaldab andmeid isikute kohta, kelle e-hääl tuleb tühistada (on paberhääletanud ja sellest tulenevalt ei lähe e-hääl arvesse valimistulemuste kokkulugemisel) või ennistada (s.t. tühistatakse eelnev tühistamine ning häälte uuesti üle lugemisel võetakse ennistatud e-hääl arvesse).

EHS rakendab tühistusnimekirja e-häälte kokkulugemisel: tühistatud isikute e-hääli arvesse ei võeta, ennistatud isikute e-hääled võetakse uuesti arvesse.

Edastatav fail on ASiC-E digikonteiner (`.asice`), mis sisaldab üht JSON-formaadis andmefaili.

## Protseduur

Tühistusnimekiri edastatakse inim-masin-protseduuriga:

1) VIS peakasutaja koostab VIS3-s tühistusnimekirja ja allkirjastab selle VIS3-s digitaalselt (ID-kaardi, Mobiil-ID või Smart-ID-ga). Iga allkirjastamine loob uue digikonteineri;

2) VIS peakasutaja laeb allkirjastatud digikonteineri VIS3-st alla ja annab selle EHS operaatorile;

3) EHS operaator laeb digikonteineri EHS-i ja rakendab tühistusnimekirja e-häälte kokkulugemisel.

## Edastatav fail

Aluseks on EHS senine liides VIS2-ga, mis on spetsifitseeritud dokumendis "IVXV protokollide kirjeldus" (v 1.5.0, IVXV-PR-1.5.0, 20.04.2019), [https://www.valimised.ee/sites/default/files/uploads/eh/IVXV-protokollid.pdf](https://www.valimised.ee/sites/default/files/uploads/eh/IVXV-protokollid.pdf), jaotises "Tühistus- ja ennistusnimekiri" (jaotis 9.1).

Valimissündmuse identifikaator peab vastama formaadile [Valimissündmuse identifikaator](../valimissündmuse_identifikaator.md).

Andmefaili struktuur (JSON-skeem): [revoke.schema](revoke.schema)

### Faili nimi

Digikonteineri nimi on kujul `<valimissündmuse identifikaator>_EVOTERS_OUTPUT_<nr>.asice`, kus `<nr>` on valimissündmuse tühistusnimekirja ekspordi järjenumber. Järjenumber algab nullist ja suureneb iga uue allkirjastatud ekspordiga ühe võrra. Suurima järjenumbriga konteiner on kõige värskem.

Konteineris olev andmefail on sama nimega, kuid laiendiga `.json`.

### Näited

Allkirjastatud digikonteinerid (ASiC-E):

- [EP_2026_ELECTION_RESULTS_EVOTERS_OUTPUT_0.asice](EP_2026_ELECTION_RESULTS_EVOTERS_OUTPUT_0.asice)
- [KOV_2026_ELECTION_RESULTS_EVOTERS_OUTPUT_0.asice](KOV_2026_ELECTION_RESULTS_EVOTERS_OUTPUT_0.asice)
- [RH_2026_ELECTION_RESULTS_EVOTERS_OUTPUT_0.asice](RH_2026_ELECTION_RESULTS_EVOTERS_OUTPUT_0.asice)
- [RK_2026_ELECTION_RESULTS_EVOTERS_OUTPUT_0.asice](RK_2026_ELECTION_RESULTS_EVOTERS_OUTPUT_0.asice)

Andmefailid (JSON):

- [revoke_EP.json](revoke_EP.json)
- [revoke_KOV.json](revoke_KOV.json)
- [revoke_RH.json](revoke_RH.json)
- [revoke_RK.json](revoke_RK.json)
