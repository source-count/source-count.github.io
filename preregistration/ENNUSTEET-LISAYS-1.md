# Lisäys 1 ennakkokirjaukseen: E3–E6:n analyysi, tulkinnat ja poikkeama

Kirjattu 2026-10-16 klo 13.42Z (mitattu `date -u`). Tämä lisäys ei muuta tiedostoa `ENNUSTEET.md` (sha256 `19e9bd7518a6979ae166862e3a1e2aabeda5215b0884e8f49b48ac8f04601ecb`, aikaleima sähköpostissa 12.41.49Z). Ennusteet ja niiden ehdot ovat ennallaan. Tämä tiedosto kirjaa poikkeaman ja kiinnittää tulkinnat, joita alkuperäinen teksti ei ratkaissut.

## Poikkeama

`ENNUSTEET.md` sanoo E3–E6:sta: "Skripti kirjoitetaan ja sen tiiviste kirjataan ennen jakson ensimmäistä keräystä."

**Näin ei tapahtunut.** Jakson ensimmäinen keräys oli käsiajo `run_a2b99754a720489ba03dd210f7f39d6c` 2026-10-16 klo 13.16.18–13.16.56Z (GO2). Analyysiskripti kirjoitettiin vasta sen jälkeen.

**Miksi tämä ei vaikuta tulokseen:** korjaus on kahden keräyksen välinen ero. Tätä kirjoittaessa keräyksiä on yksi, eikä yhdestä versiosta voi laskea yhtään korjausta. Seuraava keräys on ajastettu 17.10. klo 09.15Z. Ennen tätä lisäystä ensimmäisestä keräyksestä on nähty vain seuraavat:
- **Rivimäärät, luokkien nimet ja luokkajoukot sekä vastausten koot.** Nämä tulivat keräimen eheystarkistuksesta ja manifestista.
- **Yksiköiden tarkistus:** yhden tunnin (2026-10-10 klo 09Z) arvot aineistoista 358 (kaksi luokkaa), 124 (neljä 15 minuutin arvoa) ja 193 (neljä 3 minuutin arvoa 17:stä). Tasot olivat 358:n summa noin 5,82 GWh/h ja 124 noin 10 200 MW.

Mikään näistä ei ratkaise E3–E6:ta.

## Tulkinnat, jotka kiinnitetään nyt

1. **Arviointijakso** on keräyspäivät 2026-10-16…2026-11-14 (30 UTC-päivää). Tapaukset muodostetaan jakson sisäisistä peräkkäisistä `ok`-ajoista. Jos päivä jää väliin, parin väli on silloin pidempi. Ajot, joiden tulos on `partial`, `straddled`, `failed` tai `refused`, jätetään pois. Päivässä saa olla enintään yksi `ok`-ajo.
2. **Tapaus** on (Suomen paikallinen vuorokausi, edellinen keräyspäivä, keräyspäivä). Paikallinen aika noudattaa EU:n kesäaikasääntöä: UTC+3 maaliskuun viimeisen sunnuntain klo 01.00Z:sta lokakuun viimeisen sunnuntain klo 01.00Z:aan, muuten UTC+2. Tapauksen korjaus on tuntikorjausten summa niiltä tunneilta, jotka ovat mukana molemmissa keräyksissä molemmissa aineistoissa.
3. **Tunnin korjaus:**
   - **Datahub (358, 360, 361, 362):** luokkien summan muutos. Tunti hylätään, jos sen luokkajoukko on keräyksissä eri.
   - **124 ja 193:** MW-arvojen keskiarvon muutos niillä alijaksoilla, jotka ovat molemmissa keräyksissä, kerrottuna 1000:lla (kWh). Myöhemmin ilmestyvä alijakso ei ole korjaus.
4. **Suhde** on B/A, missä A on ensimmäinen mainittu aineisto: 358 ennusteissa E3–E5 ja 124 ennusteessa E6. Mediaani ja kvartiilit lasketaan järjestetystä listasta indekseillä `len//2`, `len//4` ja `3*len//4`, kuten `pilotti.py`:ssä. Suhde lasketaan tapauksista, joissa A ≠ 0. "Sama suunta" lasketaan tapauksista, joissa molemmat ≠ 0. "Muuttuu" tarkoittaa, että korjaus ei ole tarkalleen 0 desimaalilaskennassa.
5. **E3** jakautuu kahteen osaan: E3a (360/358) ja E3b (361/358). E3 osuu vain, jos molemmat osuvat.
6. **E5:n kynnys:** 124:n korjaus on muu kuin 0 vähintään kymmenessä E5-tapauksessa. Muuten E5 on "ei arvioitavissa".
7. **E6:n kynnys:** vähintään kymmenen tapausta, joissa molemmat korjaukset ovat muuta kuin 0. Muuten E6 on "ei arvioitavissa".
8. **Välitulokset:** ennen jakson loppua skripti tulostaa vain tapausmäärät. Tunnusluvut ja tulokset se näyttää vasta 15.11.2026 alkaen.
9. **Ennusteisiin E1–E2 tämä lisäys ei koske.** Ne arvioidaan nykyisen keräimen datasta `pilotti.py`:llä, kuten `ENNUSTEET.md` sanoo.

## Analyysi

| Tiedosto | sha256 |
|---|---|
| `analyysi_e3_e6.py` | `4380cb610e361bfe7a1d731668f7bff2f8404d8ac9d5413c8043a0361a3e6339` |
| `tests_analyysi/test_analyysi.py` | `b73edc786202a07af3710f50cb48eb0fa6c4f90ee1d93c9f6126103e848e29f0` |
| `tests_analyysi/mutaatiot.py` | `85c22f658c77ba04fd2ffdb64c9f247dd40150877f3a3337301584b0f2584636` |

**Testit:**
- 13/13 synteettisellä datalla. Oikeaa dataa testit eivät lue.
- Mutaatiot 10/10: jokainen kaatoi odotetun testin väitteeseen.
- Ensimmäisellä kierroksella kaksi testiaukkoa korjattiin ennen kirjausta:
  - Mikään testi ei vaatinut E3:n epäonnistumista. Lisättiin testit väärälle suhteelle (1,5) ja liian leveille kvartiileille.
  - Unionimutantti kaatui poikkeukseen, ei väitteeseen.

**Ajo jakson jälkeen:**
```
cd E:\HBase\skr-haku-20261016\pilotti
python -I analyysi_e3_e6.py --data-root E:\HBase-sormenjalki-data --out tulos-e3-e6.json
```

Jos skriptiä tai tulkintoja muutetaan, se kirjataan uutena lisäyksenä uudella päivämäärällä, ja muutoksen syy kerrotaan.
