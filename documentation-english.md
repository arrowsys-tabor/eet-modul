# Documentation \(English\)

### USED ABBRIVIATIONS 

DIC - Tax identification number

DIC pověřujícího - Appointing Tax identification number, special case when merchant is selling items that belong to other Tax payer.

Official government documentation for protocol: http://www.etrzby.cz/assets/cs/prilohy/EET\_popis\_rozhrani\_v3.1.1\_EN.pdf

### REQUIREMENTS

- .NET 4.5 and higher is required

### ACTIVATION OF MODULE LICENSE

1\) Fill license information to file eet-licence.txt

2\) Fill configuration file

3\) Start program \(exe\) and verify that license was successfuly verified. If license was successfuly registered, eetout.txt contains error 1005. This means that license was succesfully registered and receipt in eetin.txt was omitted and not sent.

### USING EET MODULE FROM OTHER SOFTWARE

After starting eet.exe input data are loaded from eetin.txt

in order, to detect whether process is still sendig receipts to EET, file pracuji.txt is created.

After finishing EET communication with EET server, file pracuji.txt is deleted and output is filled into eetout.txt.

In software environments which can not detect whether eet.exe is still running, pracuji.txt can be checked if exists.

When pracuji.exe does not exists, EET communication output was created.

### PLAYGROUND \(EET TEST\) ENVIRONMENT

- DIČ of sender has to be CZ1212121218 which belongs to digital certificate 01000003.p12

- Playground can be used only if 1. row of eet.txt is set to true

- Test certificates are available here http://www.etrzby.cz/cs/technicka-specifikace\)

### IMPORTANT NOTICE OF INPUT DATA

- Number fileds have to be filled with 0 even though they are empty

- Number of input rows has to be exactly the same as below

### LICENSE eet-licence.txt

1. license 

2. ICO that bought the license \(SW company\)

3. constant 1

4. license digital signature \(leave empty when registering the product\)

### CONFIGURATION eet.txt

1. debug mode - true = test environment, does not officialy records sales, false = production environment, used only with client certificates, officially records sales

2. timeout MS - minimum 2000, response timeout for EET server.

3. certificate path - system path to digital certificate

4. certificate password -  certificate password playground e.g. 01000003.p12 has password "eet"

### SENDING AND RECORDING SALES USING eetin.txt

1. prvni\_zaslani - BOOLEAN, TRUE = first send attempt, FALSE = second and each other sent attempt

2. overeni - test rezim BOOLEAN, TRUE = verification regime \(special regime that only validates date, if used, it does not returns FIK\), FALSE = used for production, officially records sales

 

\(sales record\)

3. dic\_popl - DIC of merchant, STRING 12

4. dic\_poverujiciho - DIC pověřujícího merchant, STRING 12

5. id\_provoz - ID store, INT 1-999999

6. id\_pokl - ID POS, STRING 20

7. porad\_cis - receipt number, STRING 20

8. dat\_trzba - date of sale e.g. 2016-11-09T04:2528+01:00, DATE in format ISO8601

9. celk\_trzba - total sale record, DECIMAL

10. zakl\_nepodl\_dph - Total amount for performance exempted from VAT, other performance, DECIMAL

11. zakl\_dan1 - Total tax base - basic VAT rate, DECIMAL

12. dan1 - Total VAT - basic VAT rate, DECIMAL

13. zakl\_dan2 - Total tax base - first reduced VAT rate, DECIMAL

14. dan2 - Total VAT - first reduced VAT rate, DECIMAL

15. zakl\_dan3 - Total tax base - second reduced VAT rate, DECIMAL

16. dan3 - Total VAT - second reduced VAT rate, DECIMAL

17. cest\_sluz -Total amount under the VAT scheme for travel service, DECIMAL

18. pouzit\_zboz1 - Total amount under the VAT scheme for the sale of used goods - basic VAT rate, DECIMAL

19. pouzit\_zboz2 - Total amount under the VAT scheme for the sale of used goods - first reduced VAT rate, DECIMAL

20. pouzit\_zboz3 - Total amount under the VAT scheme for the sale of used goods - second reduced VAT rate, DECIMAL

21. urceno\_cerp\_zuct -  Total amount of payments intended for subsequent drawing or settlement, DECIMAL

22. cerp\_zuct - Total amount of payments which are payments subsequently drawn or settled, DECIMAL

23. rezim - Sale regime \(FALSE - regular regime\), \(true - simplified regime which requires permit from Tax Office, allows customer to send unsent records up to 5 days\) 

### OUTPUT eetout.txt

1. porad\_cisl - receipt number, to verify

2. PKP - signature code \(is printed when FIK is not available\)

3. BKP - secure code \(has to be printed on each receipt\)

4. FIK - online code \(EET record, means that Tax Office officially recorded the sale, is printed when available\).

5. UUID - Unique identification of XML communication, do not print this on receipt, this is recommended to save to DB.

6. Error code - see errors

### ERRORS

- \(EET server errors\) see http://www.etrzby.cz/assets/cs/prilohy/EET\_popis\_rozhrani\_v3.1.1.pdf  



-1 - Docasna technicka chyba zpracovani – odeslete prosim datovou zpravu pozdeji \(system unavailable\)

0 - Datovou zpravu evidovane trzby v overovacim modu se podarilo zpracovat \(Sale record was successfully recoreded by Tax Office\)

1 - \)\*\*

2 - Kodovani XML neni platne \)\*\*\* \(invalid XML\)

3 - XML zprava nevyhovela kontrole XML schematu \(XML message does not comply with XML scheme\) This error occurs often when sale record attributes in eetin.exe are not in valid format.

4 - Neplatny podpis SOAP zpravy \(Invalid SOAP signature\)

5 - Neplatny kontrolni bezpecnostni kod poplatnika \(BKP\) \(Invalid BKP code\)

6 - DIC poplatnika ma chybnou strukturu \(invalid DIC\)

7 - Datova zprava je prilis velka \(Sale record message is too large\)

8 - Datova zprava nebyla zpracovana kvuli technicke chybe nebochybe dat \(Sale record couldn't be recorded due to technical or data error\)

9 – 999 \)\*\*

\)\* Texty chybových zpráv budou v souladu s kódováním znaků ve všech datových zprávách EET uvedeny bez diakritiky – viz 3.1 Kódování datových položek. \(Errors are send without diacritic, without special Czech characters\)

\)\*\* Rezervováno pro budoucí použití. \(Reserved for further ussage\)

\)\*\*\* Podle situace je možné na tuto chybu reagovat i navrácením technické chyby, např. tzv. SOAP fault, nebo dokonce ignorováním datové zprávy, pokud je podezření, že se jedná o kybernetický útok \(This message can occure in format e.g. SOAP fault, or request can be completely ignore when suspicious cyber attacks occur\)



Seznam chyb \(ze zpracovani EET modul\)

1001 - Internet není k dispozici \(internet unavailable\)

1002 - Chyba ověření licence \(RSA\) \(License signature error\)

1003 - Neošetřená výjimka \(Unhandled exception\)

1004 - Chybné údaje licence \(Invalid license info\)

1005 - První spuštění - EET modul byl zaregistrován, účtenka nebyla odeslána. \(Module was registered, receipt was not sent\)

1006 - Neplatná licence EET modulu. \(Invalid license\)

1007 - Překročena mezní doba odezvy \(Send timeout was reached\)

1008 - Odpověď je null \(EET response is null\)



### KREDIT

Module uses library https://github.com/l-ra/openeet

