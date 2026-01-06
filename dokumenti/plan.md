# Plan implementacije

## 1. Pregled projekta

Cilj projekta je osmisliti i implementirati sigurnosno laboratorijsko okruženje za simulaciju kibernetičkih napada korištenjem alata **Atomic Red Team**, uz analizu mrežnog prometa i sigurnosnih zapisa. Projekt omogućuje praktičnu primjenu teorijskog znanja o kibernetičkim napadima, fazama napada i obrambenim mehanizmima kroz kontrolirano testiranje u virtualnom okruženju.

Projekt se provodi u sklopu kolegija **Sigurnost informacijskih sustava**, a njegov je cilj razumjeti način na koji napadači djeluju u ranim fazama napada te kako se takve aktivnosti mogu uočiti i analizirati kroz mrežne i sigurnosne zapise.


## 2. Glavni ciljevi

1. Razviti razumijevanje metodologije Atomic Red Team i njezine povezanosti s MITRE ATT&CK okvirom.
2. Osmisliti i koristiti virtualizirano mrežno okruženje za simulaciju napada.
3. Izvesti kontrolirane napadačke testove temeljene na stvarnim napadačkim tehnikama.
4. Analizirati mrežni promet i zapise vatrozida tijekom napadačkih aktivnosti.
5. Procijeniti vidljivost i ograničenja postojećih sigurnosnih kontrola.
6. Dokumentirati rezultate testiranja i izvući zaključke o sigurnosnoj otpornosti sustava.

## 3. Struktura projekta

Projekt se sastoji od teorijskog i praktičnog dijela.

### 3.1 Teorijski dio

- Upoznavanje s konceptom Red Team i Blue Team.
- Pregled MITRE ATT&CK okvira i faza kibernetičkog napada.
- Analiza uloge Atomic Red Team alata u sigurnosnom testiranju.
- Definiranje ciljeva testiranja i opsega simuliranih napada.

### 3.2 Praktični dio

- Korištenje virtualiziranog mrežnog okruženja s:
  - LAN mrežom,
  - DMZ segmentom,
  - centralnim vatrozidom.
- Izvođenje Atomic Red Team testova s napadačkog sustava.
- Praćenje i analiza mrežnog prometa i sigurnosnih zapisa.
- Dokumentiranje rezultata i uočenih ponašanja sustava.

## 4. Plan rada po fazama

| Faza | Opis | Alati / tehnologije | Očekivani rezultat |
|------|------|---------------------|--------------------|
| 1. Analiza i priprema | Proučavanje Atomic Red Team metodologije i MITRE ATT&CK okvira. | Dokumentacija, MITRE ATT&CK | Definiran opseg testiranja |
| 2. Priprema okruženja | Postavljeno virtualno mrežno okruženje s LAN i DMZ segmentima. | VirtualBox, OPNsense | Funkcionalna infrastruktura |
| 3. Konfiguracija sigurnosti | Postavljanje firewall pravila i omogućavanje logiranja. | OPNsense | Vidljiv mrežni promet |
| 4. Izvođenje napada | Izvođenje Atomic Red Team testova. | Kali Linux, Atomic Red Team | Simulirani napadi |
| 5. Analiza | Analiza mrežnih zapisa i ponašanja sustava. | Firewall logovi | Uvid u detekcije |
| 6. Dokumentacija | Izrada završnog izvještaja i zaključaka. | Markdown / tekstualni alati | Završni rad |

## 5. Obrazloženje izbora tehnologija

| Tehnologija | Uloga u projektu | Razlog odabira |
|------------|-----------------|---------------|
| Atomic Red Team | Simulacija napada | Omogućuje male, kontrolirane i ponovljive testove |
| MITRE ATT&CK | Klasifikacija napada | Industrijski standard |
| OPNsense | Vatrozid i mrežna kontrola | Open-source, detaljno logiranje |
| Kali Linux | Napadački sustav | Standardna platforma za sigurnosno testiranje |
| VirtualBox | Virtualizacija | Reproducibilno i izolirano okruženje |

## 6. Očekivani rezultati

- Funkcionalno laboratorijsko okruženje za simulaciju kibernetičkih napada.
- Uspješno izvedeni Atomic Red Team testovi.
- Zabilježeni mrežni zapisi tijekom napadačkih aktivnosti.
- Analiza vidljivosti napadačkih tehnika u ranim fazama napada.
- Dokumentirani zaključci o sigurnosnim ograničenjima sustava.

## 7. Zaključak

Plan implementacije omogućuje sustavan i kontroliran pristup simulaciji kibernetičkih napada korištenjem Atomic Red Team alata. Projekt povezuje teorijska znanja o napadačkim tehnikama s praktičnom analizom mrežnog prometa i sigurnosnih zapisa, čime se postiže dublje razumijevanje ponašanja informacijskih sustava pod napadom te važnosti kontinuiranog sigurnosnog testiranja.

## 8. Podjela uloga u timu

Kako bi se osigurala jasna odgovornost i paralelan rad, projekt je podijeljen na četiri uloge:

- **Network Administrator - Dominik Černjević**  
  Zadužen za postavljanje i održavanje virtualne mrežne infrastrukture.  
  Aktivnosti uključuju konfiguraciju mrežnih segmenata (LAN i DMZ), povezivanje virtualnih strojeva, provjeru osnovne povezanosti te pripremu okruženja za testiranje.  
  Ključni cilj ove uloge je osigurati stabilno i reproducibilno okruženje u kojem se testovi mogu izvoditi bez mrežnih anomalija koje nisu dio napada.

- **Security Analyst - Emanuel Valec**  
  Zadužen za obrambenu stranu projekta kroz nadzor i analizu sigurnosnih zapisa tijekom napadačke faze.  
  Aktivnosti uključuju praćenje zapisa vatrozida, promatranje mrežnog prometa te interpretaciju rezultata kako bi se procijenila vidljivost napadačkih aktivnosti i ograničenja postojećih kontrola.

- **Red Team - Domagoj Gerić**  
  Zadužen za izvođenje Atomic Red Team testova i simulaciju napadačkih tehnika.  
  Aktivnosti uključuju odabir i pokretanje testova temeljenih na MITRE ATT&CK okviru te bilježenje ponašanja sustava tijekom izvođenja testova.

- **Report Writer / Presenter - Filip Podhraški**  
  Zadužen za strukturiranje projektne dokumentacije, objedinjavanje doprinosa svih članova i izradu završnog izvještaja.  
  U ovoj ulozi definira se format prikaza rezultata (opis testova, opažanja, zaključci) te priprema sadržaj za prezentaciju i obranu projekta.

## 9. Kriteriji uspješnosti projekta

Projekt se smatra uspješnim ako su ispunjeni sljedeći uvjeti:

- Atomic Red Team testovi mogu se izvesti bez narušavanja stabilnosti sustava.
- Napadačke aktivnosti ostavljaju vidljive tragove u mrežnim zapisima.
- Analiza omogućuje prepoznavanje faze otkrivanja informacija.
- Rezultati su jasno dokumentirani i interpretirani.

## 10. Ograničenja projekta

- Projekt je izveden u lokalnom virtualiziranom okruženju.
- Fokus je stavljen na rane faze napada, bez potpune kompromitacije sustava.
- Nisu implementirani napredni sustavi korelacije događaja.
