# 2 Valikute nimekiri (kandidaatide nimekiri)

## Protseduur

VIS3 edastab EHS-le andmed registreeritud kandidaatide (valimistel) või vastusevariantide (rahvahääletusel) kohta.

Andmed edastatakse inim-masin-protseduuriga:

1. VIS peakasutaja koostab VIS3-s valikute nimekirja ja allkirjastab selle VIS3-s digitaalselt (ID-kaardi, Mobiil-ID või Smart-ID-ga). Kasutaja peab valima aktiivsete valimissündmuste seast soovitud sündmuse, mille kohta nimekiri koostada. Valimissündmus on aktiivne, kui tema staatus pole `closed` ega `deleted`. Iga allkirjastamine loob uue digikonteineri;
2. VIS peakasutaja laeb allkirjastatud digikonteineri VIS3-st alla ja annab selle EHS operaatorile;
3. EHS operaator laeb digikonteineri EHS-i.

Edastatav fail on ASiC-E digikonteiner (`.asice`), mis sisaldab üht JSON-formaadis andmefaili.

## Edastatav fail

Aluseks on EHS senine liides VIS2-ga, mis on spetsifitseeritud dokumendis "IVXV protokollide kirjeldus" (v 1.5.0, IVXV-PR-1.5.0, 20.04.2019), [https://www.valimised.ee/sites/default/files/uploads/eh/IVXV-protokollid.pdf](https://www.valimised.ee/sites/default/files/uploads/eh/IVXV-protokollid.pdf), jaotises "Valikute nimekiri" (jaotis 3.4).

Valimissündmuse identifikaator peab vastama formaadile [Valimissündmuse identifikaator](../valimissündmuse_identifikaator.md).

Andmefaili struktuur (JSON-skeem): [choices.schema](choices.schema)

### Faili nimi

Digikonteineri nimi on kujul `<valimissündmuse identifikaator>_ELECTION_CHOICES_<nr>.asice`, kus `<nr>` on valimissündmuse valikute nimekirja ekspordi järjenumber. Järjenumber algab nullist ja suureneb iga uue allkirjastatud ekspordiga ühe võrra. Suurima järjenumbriga konteiner on kõige värskem.

Konteineris olev andmefail on sama nimega, kuid laiendiga `.json`.

### Näited

Allkirjastatud digikonteinerid (ASiC-E):

- [EP_2026_ELECTION_RESULTS_ELECTION_CHOICES_0.asice](EP_2026_ELECTION_RESULTS_ELECTION_CHOICES_0.asice)
- [KOV_2026_ELECTION_RESULTS_ELECTION_CHOICES_0.asice](KOV_2026_ELECTION_RESULTS_ELECTION_CHOICES_0.asice)
- [RH_2026_ELECTION_RESULTS_ELECTION_CHOICES_0.asice](RH_2026_ELECTION_RESULTS_ELECTION_CHOICES_0.asice)
- [RK_2026_ELECTION_RESULTS_ELECTION_CHOICES_1.asice](RK_2026_ELECTION_RESULTS_ELECTION_CHOICES_1.asice)

Andmefailid (JSON):

- [choices_KOV.json](choices_KOV.json)
- [choices_EP.json](choices_EP.json)
- [choices_RH.json](choices_RH.json)
- [choices_RK.json](choices_RK.json)

## Taustainfo

Valikute nimekiri sisaldab andmeid kandidaatide (valimistel) või vastusevariantide (rahvahääletusel)
kohta. Valimiste korral on lisaks kandidaadi andmetele nimekirjas ka tema erakonna või valimisliidu nimi, mille nimekirjas ta kandideerib.

Valijale elektroonilise hääletamise käigus nähtavaid valimiste vahelisi süsteemseid erinevusi on kaks:

1. Rahvahääletusel ei valita erakondadesse kuuluvate kandidaatide vahel vaid vastatakse „JAH“/“EI“ rahvahääletuse küsimusele;

2. Riigikogu, KOV ja Euroopa Parlamendi valimistel antakse hääl ühele kandidaadile, kes võib, aga ei pruugi kuuluda poliitilise ühenduse nimekirja.

Protokollistik kodeerib valija võimalikud valikud ringkonnas kuni 11-kohalise arvväärtusena, mis valikute nimekirjas kodeeritakse koos ringkonna EHAK-koodiga. Valijale tohivad kättesaadavad olla ainult tema ringkonnakohased valikud. Valijarakendus peab seda omadust tagama ning hääletamistulemust arvutav rakendus kontrollima.
