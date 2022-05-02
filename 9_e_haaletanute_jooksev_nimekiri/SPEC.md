# E-hääletanute jooksev nimekiri

kavand v0.2

## Muutelugu


- "E-hääletanute jooksev nimekiri", kavand v0.2 - Priit Parmakson, 02.05.2022
- arutelu: X-tee kasutamine, JSON - Tarmo Hanga, Priit Parmakson, apr 2022
- "EHS- VIS3 liidestus" (kavand) - Indrek Leesi, apr 2022

## Ülevaade

Käesolev spetsifikatsioon määratleb protokolli e-hääletanute nimekirja jooksvaks edastamiseks e-hääletamise süsteemist (edaspidi - EHS) Valimiste infosüsteemi (edaspidi - VIS3).

Peale hääletamise lõppu, valimispäeval edastatakse EHS-st VIS3-le e-hääletanute nimekiri (edaspidi - e-hääletanute lõplik nimekiri). See edastus on spetsifitseeritud: [E-hääletanute nimekiri](https://github.com/e-gov/VIS3-EHS/blob/main/4_e_haaletanute_nimekiri/SPEC.md). See funktsionaalsus jääb toimima - seda ei saa välja jätta, sest töötlemise viimasel etapil võivad selguda rikutud sedelid või kehtetud hääled.

Siiski on vajadus VIS3-s saada teavet, kas valija on e-hääletanud, juba enne ülalnimetatud lõplikku edastust.

E-hääletanute jooksev nimekiri edastatakse EHS-st VIS3-e X-tee teenusega.

Teenust pakub EHS. VIS3 pöördub regulaarselt teenuse poole. EHS edastab e-hääletanute andmete paki. VIS3 saab paki ja salvestab andmed VIS3 andmebaasi.

Sünkroonimiseks kasutatakse e-hääletanute nummerdamist.

## Kaalutlused

Teenus on arendatud X-tee REST võimalusi kasutades, vastavalt X-tee REST sõnumiprotokollile ([X-Road: Message Protocol for REST](https://www.x-tee.ee/docs/live/xroad/pr-rest_x-road_message_protocol_for_rest.html)). Andmed väljastatakse JSON-vormingus.

X-teed on otstarbekas kasutada, sest kuigi VIS3 ja EHS võivad olla käitatud samas taristus, on ikkagi vaja tagada usaldus, logimine ja paindlikkus - omadused, mille tagamine X-tee kasutamisega kokkuvõttes tõenäoliselt ei saaks olema lihtsam ega odavam.

Protokollis on arvesse võetud Rahvastikuregistri ja VIS3 vaheliste X-tee teenuste kasutamise kogemust (REST sõnumiprotokoll, JSON, OpenAPI).

Erilist tähelepanu on pööratud andmete re-sünkroonimise võimalusele tõrgete korral. Selleks on pakkide pärimine kavandatud idenmpotentsena.

E-hääletanute nimekirja "peegeldamiseks" EHS-st VIS3-e võiks põhimõtteliselt kasutada ka mõnda standardset sünkroonimisprotokolli (nt Git, Rsync vms, vt \[1], \[2], \[3]). Kuna vajadus on suhteliselt lihtne, siis seda ei ole tehtud. 

## E-hääletanute järjenumbrid

Tagamaks, et e-hääletanute nimekiri kantakse EHS-st VIS3-e õigeaegselt ja täielikult, kasutatakse järjenumbreid. EHS omistab igale e-hääletanule järjenumbri (Sequence Number).

Järjenumber on naturaalarv, alates ühest. Väärtus `0` tähistab olukorda, kus e-hääletanuid veel ei ole.

Igas valimissündmuses on oma numeratsioon.

## Teenus

Teenuse vastutav töötleja on Riigi Valimisteenistus. Teenust osutav süsteem on EHS.

Teenust kasutav süsteem on VIS3. Teenust kasutava süsteemi vastutav töötleja on Riigi Infosüsteemi Amet.

Teenuse ärinimi on "E-hääletanute jooksev nimekiri". Teenuse tehniline nimi (X-tee REST teenusekood, Service Code) on `e-voters-running-list`.

Teenus pakub järgmisi otspunkte:

1  `GET /elections`.  "Valimissündmuste loetelu" väljastab aktiivsete valimissündmuste loetelu. Aktiivne valimissündmus teenuse kontekstis on selline, mille kohta EHS on valmis väljastama jooksvat e-hääletanute nimekirja.

2  `GET /elections/{electionId}/lastseqno`. "Valimissündmuse viimane järjenumber" väljastab konkreetse valimissündmuse viimase EHS-s registreeritud e-hääletanu järjenumbri.

3  `GET /elections/{electionId}/evotersbatchfrom/{fromseqno}`. "e-hääletanute pakk". Selle päringuga pärib VIS3 EHS-lt valimissündmuse `{electionId}` e-hääletanute paki, alatest e-hääletanust järjenumbriga `{fromseqno}`.

Päringute ja vastuste andmestruktuuride ja samuti vastuskoodide spetsifikatsiooni vt OpenAPI spetsifikatsioonis: [ehs-xroad-api.yaml](ehs-xroad-api.yaml). 

## Otspunkt "Valimissündmuste loetelu"

Näide.

Päring: `GET /elections`

VIS3 pärib EHS-lt aktiivsete valimissündmuste loetelu.

Vastus:

```
[
  { "name": "RK_2023" }
]
```

EHS vastab, et aktiivseid valimissündmusi on üks - `RK_2023`.

Kui aktiivseid valimissündmusi ei ole, siis EHS peab vastuses saatma tühja massiivi (JSON Array).

## Otspunkt "Valimissündmuse viimane järjenumber"

Näide.

Päring: `GET /elections/RK_2023/lastseqno`

VIS3 pärib valimissündmuse `RK_2023` viimase e-hääletanu järjenumbrit. 

Vastus:

```
{
  "electionname": "RK_2023",
  "lastseqno": 54002
}
```

EHS vastab, et valimissündmuse `RK_2023` viimase e-hääletanu järjenumber on `54002`.

Kui valimissündmus on EHS-le tundmatu, siis EHS vastab HTTP vastuskoodiga `404 Not Found`.

Järjenumbrid algavad ühest (`1`). Kui valimisündmuses ei ole veel ükski valija e-hääletanud, siis vastab EHS `lastseqno` väärtusega `0`.

## Otspunkt "e-hääletanute pakk"

Näide 3.

Päring: `G /elections/RK_2023/evotersbatchfrom/54001`

VIS3 pärib valimissündmuse `RK_2023` e-hääletanute andmeid, alates järjenumbrist `54001`.

Vastus:

```
{
  "electionname": "RK_2023",
  "fromseqno": 54001,
  "batchmaxsize": 100,
  "evotersbatch": [
    { 
      "idcode": "38101010020",
      "votername": "LEO KASS",
      "seqno": 54001,
      "kovcode": "0068",
      "electoraldistrictid": 4
    },
    { 
      "idcode": "38101010021",
      "votername": "MARK KOER",
      "seqno": 54002,
      "kovcode": "0305",
      "electoraldistrictid": 4
    }
  ]

}
```

EHS vastab, et saadab valimissündmuse `RK_2023` e-hääletanute andmeid, alates järjenumbrist `54001`, pakina, milles on kuni `100` kirjet. Konkreetses pakis on kaks kirjet, kuna paki moodustamise hetkel on viimase EHS-s registreeritud e-hääletaja järjenumber `54002`. Esimene kirje tähendab, et valija `LEO KASS`, isikukoodiga `38101010020` on valimistel `RK_2023` e-hääletanud. Kirjes on ka valija KOV EHAK-kood ja valimisringkonna number.

Paki maksimaalsuuruse `batchmaxsize` määrab EHS, arvestusega, et andmed saadetakse X-tee vastussõnumi kehas (mitte manuses). Vastussõnumi töötlemisel turvaserveris loetakse keha üehaegselt põhimällu. Seetõttu ei tohi vastusõnumi keha suurus ületada 10 MB (turvaserveri vaikeseadistus).

Vastuses võib olla kuni `batchmaxsize` kirjet. Kui vastuses on kirjeid vähem kui `batchmaxsize`, siis see tähendab, et EHS-l ei ole vastuse koostamise hetkel rohkem andmeid e-hääletajate kohta.

VIS3 peab suutma töödelda erineva `batchmaxsize` väärtusega vastuseid.

# Töötluse ülevaade

EHS registreerib e-hääletamise fakte. Igale e-hääletamisele omistab EHS järjenumbri. Otstarbekas on e-hääletamise fakte hoida järjenumbri järgi indekseeritud tabelis - siis on VIS3-i päringutele vastamine kiire ja efektiivne. Paki maksimaalsuurus peaks olema EHS seadistuses määratav.

VIS3 teeb valimiste aktiivsel perioodil regulaarseid päringud EHS-i X-tee teenuse otspunkti "Valimissündmuse viimane järjenumber". EHS saadab vastuses viimase e-hääletaja järjenumbrit.

Viimase järjenumbri alusel leiab VIS3 kas VIS3-e kantud e-hääletajate andmed on EHS-iga sünkroonis. Kui viimane järjenumber osutab, et EHS-s on lisandunud kirjeid, mis vajavad VIS3-e kandmist, siis saadab VIS3 järjest päringud EHS X-tee teenuse otspunkti "e-hääletanute pakk", alates esimesest järjenumbrist, mis on VIS3-s puudu. EHS saadab paki; VIS3 salvestab saadud andmed ja saadab järgmise paki päringu.

Päringute "e-hääletanute pakk" töötlusloogika EHS-i poolel peab võimaldama VIS3-l päringuid esitada mistahes järjekorras ja kuitahes palju kordi.

Töötlus peab olema idempotentne (samajõuline) - selles mõttes, et VIS3 võib päritud andmeid igal ajal uuesti küsida. Uuesti pärimisega ei tohi tekkida duubelandmeid, tähendusnihkeid ega kinnijooksmisi.

# Veaolukordade käsitlemine

Eeldatakse, et EHS-i poolt VIS3-le väljastatav on korrektne ja muutumatu (e-hääletanute jooksva nimekirja piires). Parandus- ja muutmiskirjeid käesolev protokoll ei sisalda.

Äärmise abinõuna, juhuks kui andmeid ühe või teise osapoole või andmevahetuskanali tõrgete tõttu peaksid sünkroonist välja minema, tuleb VIS3 poolel ette valmistada võimalus e-hääletanute nimekirja täies ulatuses uuestipärimiseks. Nimetatud võimalus on kasutamiseks eriolukorras, VIS3 operaatori poolt käsitsi initsieerimisega.

# Kirjandus

\[1] Git. https://git-scm.com/.

\[2] CouchDB Replication Protocol, https://guide.couchdb.org/draft/replication.html. 

\[3] Principle and application of Rsync algorithm. https://developpaper.com/principle-and-application-of-rsync-algorithm/.