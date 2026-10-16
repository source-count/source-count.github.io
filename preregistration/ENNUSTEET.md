# Ennakkoon kirjatut ennusteet: korjausten sormenjälki

Kirjattu 2026-10-16 klo 12.37Z (mitattu `date -u`), ennen kuin arvioitavaa dataa on olemassa.

Keräystiedostossa `E:\HBase-fingrid-data\campaigns\fingrid-revision-shadow-v2\observations.jsonl` oli kirjaushetkellä 86 542 riviä (sha256 `2ec559af83a822fd0e5aa27c684adb8ac981be3c57f4083418cf71c5ac3fcd30`). Viimeinen keräys oli 15.10.2026. Pilotti (`TULOS.md`) käytti juuri nämä rivit, eikä myöhempää dataa ole nähty.

Menetelmä on `pilotti.py`, sha256 `5635153c9093fac870c38ae4a8af488c049dabac17841ad31b5df005cb9b1564`. Menetelmää ei muuteta. Jos jokin muuttuu, kirjaan uuden ennusteen uudella päivämäärällä.

## Arviointi

- **Data:** kaikki keräystiedoston rivit, joiden `recorded_at_utc` on ennen 2026-11-15T00:00:00Z. Tiedostoon vain lisätään rivejä, joten nämä rivit ovat tiedoston alku.
- **Tapaukset:** ne, joiden myöhempi keräyspäivä on 16.10.2026 tai myöhempi (`pilotti.py ... 2026-10-16`).
- **Osuma:** ennuste osuu vain, jos sen kaikki ehdot täyttyvät. Muuten se ei osu.
- **Raportointi:** kaikki ennusteet raportoidaan, myös ne, jotka eivät osu.

## E1. Samat mittarit: 358 summa vs 359 summa

a. Sama suunta vähintään 95 %:ssa tapauksista, joissa molemmat korjaukset poikkeavat nollasta.
b. Korjausten suhteen (359/358) mediaani on välillä [0,99; 1,01].
c. Suhteen ala- ja yläkvartiili ovat välillä [0,95; 1,05].

## E2. Sama järjestelmä, eri mittarit: 358 AB01 vs 358 AB02

a. Korjausten suhteen (AB02/AB01) mediaani on välin [0,8; 1,25] ulkopuolella.
b. Sama suunta alle 90 %:ssa tapauksista, joissa molemmat korjaukset poikkeavat nollasta.

## E3–E6. Uudet aineistot

Nämä arvioidaan vain, jos aineistot otetaan keräykseen. Arviointijakso on keräyksen 30 ensimmäistä päivää. Skripti kirjoitetaan ja sen tiiviste kirjataan ennen jakson ensimmäistä keräystä.

- **E3. Samat mittarit, kolmas ja neljäs jako:** 360 summa ja 361 summa vs 358 summa. Ehdot ovat samat kuin E1:ssä.
- **E4. Sama järjestelmä, eri mittarit:** 362 summa (pientuotanto) vs 358 summa. Ehdot ovat samat kuin E2:ssa.
- **E5. Eri mittausjuuri:** 124 (Fingridin oma mittaus) vs 358 summa. Jos aineisto 124 muuttuu vähintään kymmenessä tapauksessa, ehdot ovat samat kuin E2:ssa. Jos se muuttuu harvemmin, E5 on "ei arvioitavissa", ja se raportoidaan sellaisenaan.
- **E6. Sama juuri julkaisijan kuvauksen mukaan:** 124 vs 193. Jos molemmat muuttuvat vähintään kymmenessä yhteisessä tapauksessa, ennuste on sama suunta vähintään 95 %:ssa niistä. Muuten E6 on "ei arvioitavissa".
