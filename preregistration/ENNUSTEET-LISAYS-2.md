# Lisäys 2 ennakkokirjaukseen: E6:n otsikko

Kirjattu 2026-10-16 klo 15.20Z (mitattu `date -u`). Tämä lisäys ei muuta tiedostoja `ENNUSTEET.md` (sha256 `19e9bd7518a6979ae166862e3a1e2aabeda5215b0884e8f49b48ac8f04601ecb`) ja `ENNUSTEET-LISAYS-1.md` (sha256 `e30d8f8462a87955c1cae5ea4669bb3a881e9877c49975b04e7be90d6aefa9cd`). Ennusteiden ehdot, analyysiskripti ja lisäyksen 1 tulkinnat ovat ennallaan.

## Korjaus

`ENNUSTEET.md`:ssä E6:n otsikko on "Sama juuri julkaisijan kuvauksen mukaan". **Otsikko on luenta, eivätkä aineistosivut sano sitä.**

Sivut data.fingrid.fi/en/datasets/124 ja /193 luettiin 2026-10-16:
- **124:** kulutus perustuu Fingridin tuotantomittauksiin. Pieni mittaamaton osa tuotannosta arvioidaan. Kaava on tuotanto + tuonti − vienti. Yksikkö on MWh/h, ja jakso on 15 minuuttia.
- **193:** kulutus lasketaan tuotannosta ja rajasiirroista. Ne perustuvat Fingridin käytönvalvontajärjestelmän reaaliaikamittauksiin. Yksikkö on MW, ja jakso on 3 minuuttia.

Sivut kertovat saman laskukaavan ja sen, että mittaukset ovat Fingridin omia. Ne eivät kerro, ovatko mittaukset samat.

**Korjattu otsikko:** E6. Sama laskukaava julkaisijan kuvauksen mukaan: 124 vs 193.

**Ennuste on ennallaan:** jos molemmat muuttuvat vähintään kymmenessä yhteisessä tapauksessa, ennuste on sama suunta vähintään 95 %:ssa niistä. Muuten E6 on "ei arvioitavissa".

**Luenta:** E6:n tulos kertoo, korjautuvatko kaksi samalla kaavalla laskettua sarjaa samaan suuntaan. Se ei yksin ratkaise, onko mittaus sama.

## Mitä on nähty lisäyksen 1 jälkeen

- Sormenjälkidatassa on yhä vain yksi keräys: `run_a2b99754a720489ba03dd210f7f39d6c` 2026-10-16. Yhdestä versiosta ei voi laskea korjausta.
- 2026-10-16 klo 15.12Z (istuntohistorian aikaleima) luin tästä keräyksestä aineiston 362 tasot. Luin vain luokan AV06 (aurinkosähkö) päiviltä 1.–2.10.2026. Tarkoitus oli tarkistaa, että arvot ovat tuotantoa, koska sivun arvokentän kuvaus sanoo kulutusta. Tasot eivät ratkaise E4:ää.
- Grok luki 16.10. manifestista tunnisteen, ajan, tuloksen ja aineistotunnukset. Raaka-arvoja se ei lukenut. Grok ajoi `pilotti.py`:n uudelleen vain keräystiedoston 86 542 ensimmäisellä rivillä.
- Fingridin aineistosivuilla näkyy esimerkkinä uusimmat arvot. Ne ovat yksi versio, eivätkä ne kerro korjauksista.

Mikään näistä ei ratkaise E1–E6:ta.
