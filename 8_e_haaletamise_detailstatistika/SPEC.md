# 8 E-hääletamisest osavõtu detailne statistika

EHS annab seadistatud perioodiga (nt 15 min) VIS3-le hääletamisest osavõtu detailse statistika.

EHS teeb seda HTTPS päringutega VIS3 poolt pakutava otspunkti vastu.

Statistika sisaldab ka e-hääletanute koguarvu (kirje, mille `county` väärtus on `TOTAL`). Kuna koguarv ja detailandmed koostatakse EHS-is ühe ekspordina, on need omavahel alati kooskõlas.

Päringuga edastatav fail:

JSON-skeem: [online-voters-counties.schema](online-voters-counties.schema)

Valimissündmuse identifikaator peab vastama formaadile [Valimissündmuse identifikaator](../valimissündmuse_identifikaator.md).

Näide (JSON): [online-voters-counties.json](online-voters-counties.json)
