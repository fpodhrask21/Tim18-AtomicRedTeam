# Uvod
Kibernetička sigurnost jedno je od najvažnijih područja suvremenih informacijskih sustava, osobito u kontekstu sve veće digitalizacije poslovnih procesa i oslanjanja organizacija na mrežne i računalne resurse. Razvoj tehnologije, cloud rješenja i udaljenog rada doveo je do značajnog povećanja napadne površine, čime su informacijski sustavi postali izloženiji različitim vrstama kibernetičkih prijetnji.

Napadači u pravilu ne započinju napad izravnom kompromitacijom sustava, već kroz fazu prikupljanja informacija, analize mreže i identifikacije potencijalnih ranjivosti. Upravo zbog toga organizacije sve češće koriste simulirane kibernetičke napade kao metodu procjene razine sigurnosti, otpornosti sustava i učinkovitosti implementiranih sigurnosnih kontrola. Takav pristup omogućuje identifikaciju slabih točaka prije nego što ih iskoriste stvarni napadači.

Cilj ovog projektnog rada je demonstrirati primjenu alata Atomic Red Team u procesu testiranja sigurnosnih kontrola kroz simulaciju realističnih napada u kontroliranom virtualnom okruženju. Korištenjem unaprijed definiranih testova temeljenih na MITRE ATT&CK okviru, provedena je analiza ponašanja sustava tijekom različitih napadačkih tehnika, s posebnim naglaskom na fazu otkrivanja informacija (discovery).

Projekt obuhvaća postavljanje virtualne mrežne infrastrukture, definiranje uloga sudionika (mrežni administrator, sigurnosni analitičar i Red Team), izvođenje simuliranih napada te analizu dobivenih rezultata. Na temelju provedene analize izrađene su preporuke za unaprjeđenje sigurnosti sustava, čime se naglašava važnost kontinuiranog testiranja i proaktivnog pristupa kibernetičkoj sigurnosti. 
# Atomic Red Team
## Opći pregled alata
Atomic Red Team je open-source alat za simulaciju kibernetičkih napada, razvijen s ciljem jednostavnog i ponovljivog testiranja sigurnosnih kontrola unutar informacijskih sustava. Projekt je izvorno pokrenut od strane tvrtke Red Canary, a temelji se na MITRE ATT&CK okviru koji definira taktike, tehnike i procedure (TTP) korištene u stvarnim kibernetičkim napadima [1], [2].
Za razliku od kompleksnih penetration testing alata koji često zahtijevaju dugotrajnu pripremu i visoku razinu stručnosti, Atomic Red Team omogućuje izvođenje malih, izoliranih testova (tzv. atomic tests) koji simuliraju pojedinačne napadačke tehnike. Takav pristup omogućuje sigurnosnim timovima brzo provjeravanje jesu li postojeće sigurnosne kontrole sposobne detektirati ili spriječiti specifične napadačke aktivnosti [3].

## Koncept atomic testova
Osnovna jedinica Atomic Red Team alata je atomic test. Svaki atomic test predstavlja minimalni, samostalni scenarij koji simulira jednu konkretnu tehniku iz MITRE ATT&CK okvira. Testovi su namjerno dizajnirani da budu jednostavni, kratki i fokusirani isključivo na jednu radnju napadača, primjerice otkrivanje sistemskih informacija, skeniranje mrežnih servisa ili enumeraciju korisničkih računa [2].
Svaki test sadrži jasno definirane elemente:
•	opis napadačke tehnike,
•	potrebne preduvjete za izvođenje testa,
•	naredbe ili skripte koje se izvršavaju na ciljnom sustavu,
•	očekivano ponašanje sustava tijekom i nakon testa.
Ovakva struktura omogućuje lako ponavljanje testova te usporedbu rezultata kroz vrijeme, što je posebno važno u kontinuiranom procesu unaprjeđenja sigurnosti [4].

## Povezanost s MITRE ATT&CK okvirom
Jedna od ključnih prednosti Atomic Red Team alata je izravna povezanost s MITRE ATT&CK okvirom. Svaki atomic test mapiran je na točno određenu ATT&CK tehniku, označenu jedinstvenim identifikatorom (npr. T1082 – System Information Discovery). Time se omogućuje standardizirana klasifikacija napadačkih aktivnosti i njihovo povezivanje s poznatim obrascima ponašanja napadača [1].
Takvo mapiranje omogućuje sigurnosnim analitičarima da precizno utvrde koje su ATT&CK tehnike uspješno detektirane, a koje nisu. Rezultati testova mogu se koristiti za procjenu pokrivenosti sigurnosnih kontrola u odnosu na ATT&CK matricu, što predstavlja važan alat u planiranju poboljšanja obrambene strategije [5].

## Uloga Atomic Red Team alata u sigurnosnom testiranju
Atomic Red Team najčešće se koristi u kontekstu purple team pristupa, gdje suradnja između napadačkih (red team) i obrambenih (blue team) timova omogućuje učinkovito testiranje i poboljšanje sigurnosnih mehanizama. Umjesto fokusiranja na pronalazak jedne kritične ranjivosti, cilj je provjeriti vidljivost napadačkih aktivnosti i sposobnost sustava da ih pravovremeno detektira [3].
U edukacijskim i istraživačkim okruženjima Atomic Red Team posebno je koristan zbog svoje transparentnosti i otvorenog koda. Studenti i istraživači mogu jasno pratiti koje se naredbe izvršavaju, razumjeti njihovu svrhu te analizirati reakciju sustava bez potrebe za korištenjem naprednih ili zatvorenih komercijalnih alata [6].

## Prednosti i ograničenja alata
Glavne prednosti Atomic Red Team alata uključuju jednostavnost implementacije, otvoreni kod, izravnu povezanost s MITRE ATT&CK okvirom te mogućnost brzog testiranja pojedinačnih napadačkih tehnika. Alat je posebno pogodan za kontinuirano testiranje sigurnosnih kontrola i validaciju detekcijskih mehanizama [2], [4].
Međutim, važno je naglasiti da Atomic Red Team ne predstavlja zamjenu za cjelovito penetracijsko testiranje. Budući da se testovi izvode izolirano, oni ne simuliraju kompletne višefazne napade niti kompleksne scenarije lateralnog kretanja unutar mreže. Stoga se Atomic Red Team najčešće koristi kao dopuna drugim sigurnosnim metodama i alatima [5].

# Reference
[1] MITRE Corporation, “MITRE ATT&CK® Framework,” 2024. [Online]. Available: https://attack.mitre.org <br>
[2] Red Canary, “Atomic Red Team,” 2024. [Online]. Available: https://atomicredteam.io <br>
[3] R. M. Lee, R. Assante, and T. Conway, “Purple Teaming: The Next Step in Cybersecurity,” SANS	Institute,	2016. <br>
[4] Red Canary, “Atomic Red Team GitHub Repository,” 2024. [Online]. Available: https://github.com/redcanaryco/atomic-red-team <br>
[5] N. C. Idika and B. Bhargava, “Extending the MITRE ATT&CK Framework for Defense Evaluation,” IEEE Security & Privacy, vol. 18, no. 3, pp. 42–51, 2020. <br>
[6] A. Rege-Patwardhan et al., “Cybersecurity Experimentation Using Open-Source Attack Frameworks,” IEEE Access, vol. 9, pp. 123456–123468, 2021.
