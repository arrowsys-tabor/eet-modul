# Dokumentace

### POŽADAVKY

* .NET 4.5 a vyšší
* Sada zkušební EET certifikátu je ke stažení na [http://www.etrzby.cz/assets/cs/prilohy/EET\\_CA1\\_Playground\\_v1.zip](http://www.etrzby.cz/assets/cs/prilohy/EET\_CA1\_Playground\_v1.zip) popřípadě http://www.etrzby.cz/cs/technicka-specifikace

### POSTUP AKTIVACE LICENCE

1\) Vyplnit licenční údaje v souboru eet-licence.txt

2\) Nastavit konfigurační soubor

3\) Spustit program a ověřit zda byla licence řádně zaregistrována

### PROPOJENÍ S NADSTRAVBOVÝM SW

Po spuštění eet.exe se načtou údaje o evidované tržbě z eetin.txt

paralelně se vytvoří soubor pracuji.txt.

Po ukončení odesílání se soubor pracuji.txt smaže a výsledek bude zapsán do eetout.txt.

V programových prostředích, které neumožnují sledování procesů je možné použít pracuji.txt

pro zjištění zdali proces odesílání již skončil.

### INFORMACE PRO PLAYGROUND

* DIČ odesílatele musí být CZ1212121218 na které je vystaven certifikát 01000003.p12

* Do Playground lze odesílat pouze pokud je 1. řádek eet.txt nastaven na true

**DŮLEŽITÉ**

* Číselné položky musejí být vyplněné i pokud obsahují 0

* Počet řádků vstupních souborů musí být zachován

**LICENCE eet-licence.txt**

1. cislo licence

2. ICO na ktere je licence registrovana

3. Číslo Stanice - konstanta 1. Pokud se instalujte na další stanici pod stejným IČ, je zapotřebí **číslo zvýšit**.

4. radek pro overeni \(nevyplnuje se\)

### KONFIGURACE eet.txt

1. debug mode - true = neprodukční prostředí, lze použít pouze certifikáty pro playground, false = produkční prostředí nastavte vždy na false, lze použít pouze ostré certifikáty

2. timeout MS - minimum 2000, casovy limit pro cekani na odpoved ze serveru EET.

3. certificate path - systémová cesta k elektronickému certifikátu, ve zkušební verzi je dodáván od MFČR soubor 01000003.p12 s heslem "eet". Cesta nesmí obsahovat diakritiku, speciální znaky a podtržitko.

4. certificate password

### ODESLÁNÍ TRŽBY HLAVICKA eetin.txt

1. prvni\_zaslani - BOOLEAN, TRUE = prvni zaslani, FALSE = opetovne

2. overeni - test rezim BOOLEAN, TRUE = overovaci rezim \(vraci z MFCR misto FIK zpravu zdali jsou parametry OK evidenci trzev\), FALSE = evidovat trzbu \(udaje o samotne trzbe\)

3. dic\_popl - DIC od koho tržba plyne STRING 12

4. dic\_poverujiciho - DIC povereneho odesilatele trzby STRING 12

5. id\_provoz - ID provozovny INT 1-99999

6. id\_pokl - ID pokladny STRING 20

7. porad\_cis - pořadové číslo účtenky STRING 20

8. dat\_trzba - datum kdy se trzba uskutecnila ve formatu 2016-11-09T04:2528+01:00 formát ISO8601

9. celk\_trzba - celkovy soucet trzby DECIMAL

10. zakl\_nepodl\_dph - celkvá částka plnění osvbozených od DPH DECIMAL

11. zakl\_dan1 - celkový základ daně se základní sazbou DPH

12. dan1 - celková DPH se základní sazbou

13. zakl\_dan2 - celkový základ daně s první sníženou sazbou DPH

14. dan2 - celková DPH s první sníženou sazbou

15. zakl\_dan3 - celkový  základ daně s druhou sníženou sazbou DPH

16. dan3 - celková DPH s druhou sníženou sazbou

17. cest\_sluz - celková částka v režimu DPH pro cestovní službu

18. pouzit\_zboz1 - celková částka v režimu DPH pro prodej použitého zboží se základní sazbou

19. pouzit\_zboz2 - celková částka v režimu DPH pro prodej použitého zboží s první sníženou sazbou

20. pouzit\_zboz3 - celková částka v režimu DPH pro prodej použitého zboží s druhou sníženou sazbou

21. urceno\_cerp\_zuct -  celková částka plateb určená k následnému čerpání nebo zúčtování

22. cerp\_zuct - celková částka plateb které jsou následným čerpáním nebo zúčtováním platby

23. rezim - FALSE - běžný režim, true - zjednodušený režim

**VYSLEDEK eetout.txt**

1. porad\_cisl - zpetna kontrola odeslané učtenky

2. PKP - offline zprava \(tiskne se pokud neni FIK\)

3. BKP - offline kod \(tiskne se vzdy\)

4. FIK - online kod \(tiskne se vzdy pokud je k dispozici\) V ověřovacím režimu obashuje zprávu ze serveru MFČR zdali zasílané parametry jsou jsou validní.

5. UUID - unikátní kód návratové zprávy ze serveru EET

6. Kód a popis chyby viz chybář

### SEZNAM CHYB

* \(z odpovedi EET serveru\) viz [http://www.etrzby.cz/assets/cs/prilohy/EET\\_popis\\_rozhrani\\_v3.1.1.pdf](http://www.etrzby.cz/assets/cs/prilohy/EET\_popis\_rozhrani\_v3.1.1.pdf)  

-1 - Docasna technicka chyba zpracovani – odeslete prosim datovou zpravu pozdeji

0 - Datovou zpravu evidovane trzby v overovacim modu se podarilo zpracovat

1 - \)\*\*

2 - Kodovani XML neni platne \)\*\*\*

3 - XML zprava nevyhovela kontrole XML schematu

4 - Neplatny podpis SOAP zpravy

5 - Neplatny kontrolni bezpecnostni kod poplatnika \(BKP\)

6 - DIC poplatnika ma chybnou strukturu

7 - Datova zprava je prilis velka

8 - Datova zprava nebyla zpracovana kvuli technicke chybe nebochybe dat

9 – 999 \)\*\*

\)\* Texty chybových zpráv budou v souladu s kódováním znaků ve všech datových zprávách EET uvedeny bez diakritiky – viz 3.1 Kódování datových položek.

\)\*\* Rezervováno pro budoucí použití.

\)\*\*\* Podle situace je možné na tuto chybu reagovat i navrácením technické chyby, např. tzv. SOAP fault, nebo dokonce ignorováním datové zprávy, pokud je podezření, že se jedná o kybernetický útok

Seznam chyb \(ze zpracovani EET modul\)

1001 - Internet není k dispozici

1002 - Chyba ověření licence \(RSA\)

1003 - Neošetřená výjimka

1004 - Chybné údaje licence

1005 - První spuštění - EET modul byl zaregistrován, účtenka nebyla odeslána.

1006 - Neplatná licence EET modulu.

1007 - Překročena mezní doba odezvy

1008 - Odpověď je null

### KREDIT

Aplikace vyuziva knihovnu [https://github.com/l-ra/openeet](https://github.com/l-ra/openeet)

