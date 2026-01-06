# Setup – Sigurnosno mrežno okruženje (OPNsense)

Ovaj dokument opisuje postupak postavljanja i konfiguracije virtualnog mrežnog okruženja korištenog u projektu **Atomic Red Team**. Cilj okruženja je omogućiti realističnu simulaciju poslovne mreže u kojoj je moguće sigurno provoditi napadačke scenarije, pratiti mrežni promet te analizirati sigurnosne događaje na razini vatrozida.

Mrežno okruženje temelji se na **OPNsense vatrozidu**, koji ima ulogu središnje točke kontrole prometa, segmentacije mreže i prikupljanja log zapisa. Konfiguracija je prilagođena tako da istovremeno omogućuje funkcionalnost sustava i visoku razinu vidljivosti napadačkih aktivnosti, što je ključno za ulogu sigurnosnog analitičara.

## Virtualno okruženje i arhitektura

Cijeli sustav implementiran je unutar **VirtualBox** virtualizacijskog okruženja. Korištenjem virtualnih strojeva omogućeno je izolirano i sigurno testiranje sigurnosnih scenarija bez rizika za stvarnu infrastrukturu.

Okruženje se sastoji od sljedećih virtualnih strojeva:

- **OPNsense Firewall** – centralni mrežni uređaj koji provodi segmentaciju, filtriranje i bilježenje prometa  
- **Workstation 1 (LAN)** – korisnička radna stanica i sustav za analizu logova  
- **Workstation 2 (LAN)** – dodatna korisnička stanica (nije nužna za izvođenje napada)  
- **Kali Linux (LAN)** – napadačka platforma (Red Team)  
- **Ubuntu Server (DMZ)** – ciljni poslužitelj s aktivnim mrežnim servisima  

Mrežna arhitektura podijeljena je u dvije sigurnosne zone:

- **LAN (Local Area Network)** – interna mreža s korisničkim sustavima i napadačkom platformom  
- **DMZ (Demilitarized Zone)** – mreža s poslužiteljima izloženima povećanom sigurnosnom riziku  

Takva segmentacija predstavlja standardnu sigurnosnu praksu jer omogućuje kontrolu prometa između mrežnih zona i smanjuje rizik širenja napada.

## Inicijalna konfiguracija OPNsense sustava

Nakon pokretanja OPNsense virtualnog stroja provedena je osnovna konfiguracija putem konzolnog sučelja. U ovoj fazi definirana su mrežna sučelja, IP adresiranje te osnovne mrežne funkcionalnosti.

Dodijeljena su sljedeća mrežna sučelja:

- **WAN** – povezan na NAT adapter, koristi se za pristup internetu  
- **LAN** – interna mreža za korisničke sustave  
- **OPT1 (DMZ)** – zasebna mreža za poslužitelje izložene povećanom riziku  

LAN sučelju dodijeljena je IP adresa `192.168.10.1/24`, dok je DMZ sučelje konfigurirano s adresom `172.16.1.1/24`. Na oba sučelja aktiviran je DHCP poslužitelj kako bi se pojednostavila mrežna konfiguracija klijentskih sustava.

## Pristup web administracijskom sučelju

Nakon osnovne konfiguracije omogućen je pristup OPNsense web sučelju putem HTTPS protokola. Administratorsko sučelje dostupno je s LAN mreže na adresi: https://192.168.10.1

Tijekom inicijalnog čarobnjaka konfigurirani su osnovni parametri sustava, uključujući naziv sustava, vremensku zonu, DNS postavke te administratorske vjerodajnice. Ovim korakom osigurana je stabilna i dosljedna osnovna konfiguracija sustava.

## Konfiguracija mrežnih sučelja i segmentacije

Sučelje OPT1 preimenovano je u **DMZ** kako bi se jasno razlikovala njegova uloga unutar sustava. Time je dodatno naglašena segmentacija mreže između interne zone i zone s izloženim servisima.

Ovakva podjela omogućuje:

- preciznu kontrolu prometa između mrežnih zona  
- jasnu analizu pokušaja pristupa DMZ sustavima  
- jednostavnije definiranje i razumijevanje firewall pravila  

## Firewall pravila i kontrola prometa

Firewall pravila predstavljaju ključni sigurnosni element cijelog okruženja. Pravila su definirana tako da omoguće funkcionalnost sustava, ali istovremeno jasno ograniče neovlaštenu komunikaciju.

### LAN pravila

Na LAN sučelju dopušten je sav izlazni promet. Ovakva konfiguracija omogućuje korisničkim sustavima i napadačkoj platformi slobodnu komunikaciju prema ostalim mrežnim segmentima i internetu. Time se simulira realističan scenarij u kojem napadač već ima inicijalni pristup internoj mreži.

### DMZ pravila

DMZ sučelje konfigurirano je znatno restriktivnije. Dopušten je samo unaprijed definiran skup servisa iz LAN mreže, uključujući:

- SSH (22)  
- HTTP (80)  
- HTTPS (443)  
- FTP (21)  
- MySQL (3306)  

Svi ostali pokušaji komunikacije automatski se blokiraju i bilježe u firewall logovima.

Ovakav pristup omogućuje:

- smanjenje površine napada  
- jasnu vidljivost pokušaja neovlaštenog pristupa  
- analizu firewall logova tijekom izvođenja napada  

## NAT i pristup internetu

Outbound NAT konfiguriran je u **Hybrid mode**, čime je omogućeno da sustavi iz LAN i DMZ mreže imaju pristup internetu, dok sav promet prolazi kroz OPNsense vatrozid. Time je osigurana dodatna kontrola i mogućnost nadzora izlaznog prometa.

## DHCP i DNS konfiguracija

DHCP poslužitelj aktivan je na oba mrežna segmenta kako bi se osigurala jednostavna mrežna konfiguracija klijentskih sustava. DNS rezolucija osigurana je korištenjem **Unbound DNS resolvera**, koji je konfiguriran da sluša na LAN i DMZ sučeljima.

Dodatno je omogućena:

- DNSSEC validacija  
- automatska registracija DHCP leaseova  

Time je osigurana pouzdana i sigurna DNS infrastruktura unutar okruženja.

## Logging i nadzor sigurnosnih događaja

Za potrebe uloge sigurnosnog analitičara omogućeno je detaljno logiranje mrežnog prometa. OPNsense bilježi:

- sve blokirane pakete  
- promet koji prolazi kroz zadana pass pravila  

Log zapisi dostupni su u stvarnom vremenu putem web sučelja, što omogućuje trenutačnu analizu ponašanja sustava tijekom izvođenja Atomic Red Team testova i ručnih mrežnih skeniranja.

## Testiranje ispravnosti konfiguracije

Nakon dovršetka konfiguracije provedeni su osnovni testovi povezanosti i funkcionalnosti. Testirana je komunikacija prema gatewayu, internetu, DNS rezolucija te pristup DMZ poslužitelju.

Svi testovi potvrdili su ispravnu konfiguraciju mreže i firewall pravila.

## Snapshot i priprema za testiranje napada

Nakon potvrde stabilnosti sustava napravljeni su snapshoti svih virtualnih strojeva. Time je osigurana mogućnost brzog povratka sustava u početno stanje, što je ključno za ponovljivo izvođenje napadačkih scenarija.

Okruženje je u ovom stanju potpuno spremno za:

- izvođenje Atomic Red Team testova  
- analizu firewall logova  
- evaluaciju vidljivosti napadačkih aktivnosti  

## Zaključak

Postavljeno sigurnosno mrežno okruženje predstavlja funkcionalnu i realističnu simulaciju poslovne infrastrukture u kojoj su jasno odvojene sigurnosne zone, definirana pravila mrežne komunikacije i omogućeno detaljno praćenje sigurnosnih događaja. Korištenjem OPNsense vatrozida kao središnjeg elementa sustava ostvarena je učinkovita kontrola prometa između interne mreže i demilitarizirane zone, uz istovremeno osiguravanje vidljivosti napadačkih aktivnosti na mrežnoj razini.

Implementirana segmentacija mreže i strogo definirana firewall pravila dokazala su se kao učinkovita prva linija obrane jer uspješno ograničavaju neovlaštenu komunikaciju i smanjuju površinu napada. Analiza firewall logova pokazuje da sustav pouzdano bilježi pokušaje pristupa nedopuštenim servisima i mrežnim segmentima, čime se sigurnosnom analitičaru omogućuje uvid u ponašanje napadača tijekom izvođenja simuliranih napada.

Istovremeno, ovakvo okruženje jasno ilustrira ograničenja sigurnosti temeljene isključivo na mrežnim pravilima. Iako vatrozid učinkovito provodi zadane politike, nedostatak naprednijih mehanizama za korelaciju događaja i analizu ponašanja otežava rano prepoznavanje napadačkih obrazaca. Time se potvrđuje da mrežna segmentacija i firewall, iako nužni, sami po sebi nisu dovoljni za detekciju sofisticiranijih prijetnji.
