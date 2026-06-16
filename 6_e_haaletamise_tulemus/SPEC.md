# E-hääletamise tulemus

E-hääletamise lugemisprotseduuri tulemusena arvutab EHS e-hääletamise tulemuste
faili (hääletamistulemuse fail) ning signeerib selle (hääletamistulemuse 
signatuuri fail) valimiskomisjoni kontrolli all oleva privaatvõtmega. Failid laetakse
VIS3-e (valimistulemuse moodulisse TUL).


## Protseduur

Fail edastatakse inim-masin-protseduuriga:

1. EHS operaator kopeerib hääletamistulemuse faili, hääletamistulemuse
   signatuuri faili ning valimiskomisjoni avaliku võtme faili lugemisrakenduse
   väljundist;

2. EHS operaator allkirjastab failid digitaalselt väljaspool EHS-i ja annab
   allkirjastatud konteineri VIS peakasutajale;

3. VIS peakasutaja laeb allkirjastatud konteineri VIS3-e.


VIS3-e poolel järgnevad allkirjastatud konteineri laadimisele järgmised tegevused:

1. Allkirjastatud konteineri valideerimine SIGA teenusega

2. Allkirjastatud failide eraldamine

3. Hääletamistulemuse signatuuri kontrollimine valimiskomisjoni avaliku võtme abil.


## Edastatav fail

Hääletamistulemuse faili nimi on kujul:
`<election_code>.<election_question>.tally.json`

Hääletamistulemuse signatuuri faili nimi on kujul:
`<election_code>.<election_question>.tally.json.signature`

Valimiskomisjoni avaliku võtme faili nimi on kujul: `<election_code>-sign.pub`

Valimissündmuse identifikaator `<election_code>` ja küsimuse identifikaator
`<election_question>` peavad vastama formaadile [Valimissündmuse
identifikaator](../valimissündmuse_identifikaator.md).

Hääletamistulemuse faili struktuur (JSON-skeem): [results.schema](results.schema)

Hääletamistulemuse faili näited (JSON):

- [EP.1.tally.json](EP.1.tally.json) - sündmus EP, küsimus 1
- [KOV.1.tally.json](KOV.1.tally.json) - sündmus KOV, küsimus 1
- [RH.1.tally.json](RH.1.tally.json) - sündmus RH, küsimus 1
- [RK.1.tally.json](RK.1.tally.json) - sündmus RK, küsimus 1


## Hääletamistulemuse signatuuri kontrollimine

Hääletamistulemuse signatuuri kontrollimiseks automatiseeritakse järgmine e-hääletamise käsiraamatus kirjeldatud protseduur:

```
openssl dgst -sha256 -sigopt rsa_padding_mode:pss -sigopt rsa_pss_saltlen:32 -sigopt
rsa_mgf1_md:sha256 -verify <election_code>-sign.pub -signature <election_code>.<election_question>.tally.json.signature <election_code>.<election_question>.tally.json 
```

