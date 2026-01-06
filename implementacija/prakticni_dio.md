# Praktični dio
## Opis virtualnog mrežnog okruženja
Virtualno mrežno okruženje korišteno u ovom projektu osmišljeno je s ciljem simulacije realne poslovne infrastrukture kakva se može pronaći u malim i srednjim organizacijama. Poseban naglasak stavljen je na jasno razdvajanje sigurnosnih zona, kontrolu mrežnog prometa te mogućnost praćenja napadačkih aktivnosti unutar različitih dijelova mreže. Okruženje je u potpunosti virtualizirano, čime je omogućeno sigurno izvođenje napada bez rizika za stvarne sustave.
Mrežna topologija podijeljena je u dvije osnovne sigurnosne zone: internu mrežu (LAN) i demilitariziranu zonu (DMZ). Takav model segmentacije predstavlja standardnu sigurnosnu praksu u organizacijama jer omogućuje izolaciju kritičnih resursa od sustava koji su izloženi većem riziku. Segmentacija je provedena korištenjem OPNsense vatrozida, koji ima ulogu središnjeg mrežnog uređaja zaduženog za filtriranje, nadzor i bilježenje prometa između pojedinih mrežnih segmenata.
Interna LAN mreža namijenjena je korisničkim sustavima i internim resursima. U ovom segmentu nalaze se dvije radne stanice koje simuliraju krajnje korisnike te jedan sustav s instaliranim Kali Linux operativnim sustavom. Kali Linux sustav preuzima ulogu napadačke platforme (Red Team) i koristi se za izvođenje simuliranih kibernetičkih napada. Smještanjem napadačke platforme unutar LAN segmenta simulira se scenarij u kojem je napadač već ostvario inicijalni pristup mreži, primjerice putem kompromitiranog korisničkog računala.
DMZ segment sadrži poslužitelj s aktivnim mrežnim servisima, koji predstavlja primarnu metu napada. Poslužitelj je konfiguriran tako da nudi osnovne servise, čime se simulira tipičan poslovni poslužitelj izložen mrežnom prometu. Ovakav raspored omogućuje testiranje kako mrežna segmentacija i vatrozid utječu na vidljivost i ograničavanje napadačkih aktivnosti.

## Uloge sudionika i podjela odgovornosti
Kako bi se simulirao realan radni scenarij unutar organizacije, projekt je podijeljen prema ulogama sudionika. Svaka uloga ima jasno definirane odgovornosti unutar procesa planiranja, izvođenja i analize simuliranih napada.
Mrežni administrator bio je zadužen za dizajn i implementaciju virtualne mrežne infrastrukture. Njegove odgovornosti uključivale su konfiguraciju virtualnih strojeva, postavljanje IP adresiranja, definiranje mrežnih segmenata te osnovnu konfiguraciju vatrozida.
Sigurnosni analitičar imao je zadatak konfigurirati sigurnosne kontrole te pratiti ponašanje sustava tijekom simuliranih napada. To je uključivalo analizu mrežnog prometa, pregled log zapisa te procjenu učinkovitosti postojećih sigurnosnih mehanizama.
Red Team je koristio Kali Linux i Atomic Red Team alat za izvođenje simuliranih napada. Cilj ove uloge bio je primijeniti unaprijed definirane ATT&CK tehnike te promatrati reakciju sustava bez namjernog oštećenja infrastrukture.
## Konfiguracija napadačke i ciljne infrastrukture
Napadačka infrastruktura u ovom projektu temelji se na Kali Linux operativnom sustavu, koji je široko prihvaćen kao standardna platforma za sigurnosna testiranja i penetracijske testove. Kali Linux sadrži velik broj unaprijed instaliranih alata namijenjenih analizi mreža, testiranju ranjivosti i simulaciji napada. U sklopu ovog projekta, na Kali Linux sustavu konfiguriran je Atomic Red Team alat, koji omogućuje izvođenje pojedinačnih atomic testova povezanih s MITRE ATT&CK tehnikama.
Atomic Red Team testovi izvođeni su izravno s napadačke platforme, bez dodatnih prilagodbi koda, kako bi se zadržala autentičnost alata i omogućila ponovljivost eksperimenata. Napadačka platforma ima mrežnu povezanost prema ciljnim sustavima unutar LAN i DMZ segmenata, pri čemu sav promet prolazi kroz OPNsense vatrozid. Time je omogućeno praćenje i analiza mrežnih aktivnosti generiranih tijekom izvođenja testova.
Ciljna infrastruktura sastoji se od korisničkih radnih stanica i poslužitelja u DMZ zoni. Sustavi su namjerno konfigurirani s osnovnim sigurnosnim postavkama, bez implementacije naprednih obrambenih mehanizama poput IDS/IPS sustava ili centraliziranog SIEM rješenja. Takav pristup omogućuje analizu osnovne razine sigurnosti i vidljivosti napadačkih aktivnosti u minimalno zaštićenom okruženju.
OPNsense vatrozid konfiguriran je s pravilima koja dopuštaju osnovnu komunikaciju između mrežnih segmenata, uz istovremeno bilježenje mrežnog prometa. Time je osigurana mogućnost detaljne analize pokušaja skeniranja, pristupa servisima i ostalih aktivnosti koje proizlaze iz izvođenja atomic testova.

## Izvedeni Atomic Red Team testovi
U okviru praktičnog dijela projekta provedeni su odabrani Atomic Red Team testovi koji pripadaju fazi otkrivanja informacija (discovery) prema MITRE ATT&CK okviru. Faza otkrivanja informacija predstavlja jednu od najvažnijih faza napadačkog procesa jer omogućuje napadaču razumijevanje ciljnog okruženja i identifikaciju potencijalnih točaka napada.
Test System Information Discovery (T1082) korišten je za prikupljanje informacija o operacijskom sustavu ciljanih računala. Ovim testom simulira se napadačka aktivnost usmjerena na otkrivanje verzije operacijskog sustava, arhitekture, konfiguracijskih parametara i ostalih sistemskih informacija koje mogu utjecati na izbor daljnjih napadačkih tehnika.
Test File and Directory Discovery (T1083) usmjeren je na pregled strukture datotečnog sustava. Cilj ovog testa je simulirati pokušaj pronalaska osjetljivih datoteka, konfiguracijskih zapisa ili korisničkih direktorija koji mogu sadržavati vrijedne informacije. Takvi podaci često predstavljaju polazišnu točku za eskalaciju privilegija ili daljnju kompromitaciju sustava.
Testovi Network Service Discovery korišteni su za identifikaciju aktivnih mrežnih servisa i otvorenih portova na ciljnim sustavima. Ovakvi testovi omogućuju napadaču uvid u dostupne servise te pomažu u određivanju potencijalnih vektora napada.
Konačno, test Account Discovery korišten je za otkrivanje postojećih korisničkih računa na sustavu. Informacije o korisničkim računima mogu se iskoristiti za ciljane napade, pokušaje pogađanja lozinki ili eskalaciju privilegija. Svaki test izvođen je zasebno, čime je omogućena jasna izolacija pojedinih napadačkih tehnika i preciznija analiza njihovog učinka.

## Metodologija izvođenja i prikupljanja podataka
Izvođenje simuliranih napada provedeno je prema unaprijed definiranoj metodologiji s ciljem osiguravanja dosljednosti, ponovljivosti i transparentnosti rezultata. Svaki Atomic Red Team test izvođen je kao samostalan eksperiment, pri čemu su prije i nakon izvođenja zabilježeni relevantni parametri sustava.
Tijekom izvođenja testova prikupljani su podaci o mrežnom prometu, zapisima vatrozida te ponašanju ciljanih sustava. Posebna pažnja posvećena je praćenju vidljivosti napadačkih aktivnosti, odnosno mogućnosti da sigurnosni mehanizmi zabilježe ili ograniče sumnjive radnje. Time je omogućena procjena osnovne razine detekcije napada u postojećoj konfiguraciji sustava.
Nakon završetka svakog testa provedena je analiza rezultata u kojoj su uspoređeni očekivani ishodi s stvarnim ponašanjem sustava. Dobiveni podaci korišteni su kao temelj za evaluaciju učinkovitosti sigurnosnih kontrola te za izradu preporuka za njihovo poboljšanje. Ovakav metodološki pristup omogućuje sustavno razumijevanje sigurnosnih slabosti i jasno povezivanje rezultata praktičnog dijela s analizom koja slijedi u sljedećem poglavlju.

# Analiza rezultata
Analiza rezultata temelji se na stvarnim izlazima Atomic Red Team testova, ručnim mrežnim skeniranjima te zapisima vatrozida OPNsense. Cilj analize nije dokazivanje uspješnosti napada, već procjena vidljivosti napadačkih aktivnosti i učinkovitosti postojećih sigurnosnih kontrola u fazi otkrivanja informacija (discovery).
Za potrebe analize korišteni su terminalski ispisi s Kali Linux sustava te log zapisi vatrozida, koji su dokumentirani pomoću priloženih snimki zaslona.

## Analiza testa System Information Discovery (T1082)
Test System Information Discovery (T1082) izvršen je korištenjem Atomic Red Team alata na ciljnom Linux sustavu. Kao što je prikazano na Slici 1, test je uspješno dohvatilo detaljne informacije o operacijskom sustavu, uključujući naziv distribucije, verziju kernela, arhitekturu sustava i osnovne sistemske parametre.
 
<img width="945" height="591" alt="image" src="https://github.com/user-attachments/assets/6ff56511-5b57-4247-a115-cd19e68949b8" />
<p><em>Slika 1: Izlaz Atomic Red Team testa T1082 – System Information Discovery</em></p>
Dobiveni rezultati ukazuju na to da napadač može bez prepreka prikupiti ključne informacije o sustavu. Takve informacije predstavljaju temelj za daljnje faze napada jer omogućuju prilagodbu napadačkih alata i tehnika specifičnom okruženju. Tijekom izvođenja testa nije zabilježena aktivna blokada niti upozorenje na razini sustava, što upućuje na nedostatak lokalnih mehanizama za detekciju ove vrste aktivnosti.

## Analiza testa File and Directory Discovery (T1083)
Test File and Directory Discovery (T1083) korišten je za pregled strukture datotečnog sustava. Na Slici 2 vidljiv je ispis direktorija i datoteka dobiven izvršavanjem Atomic Red Team testa, čime je simuliran pokušaj pronalaska potencijalno osjetljivih podataka.
 
<img width="945" height="591" alt="image" src="https://github.com/user-attachments/assets/d7c65a17-bd6e-4465-b266-9b155d350241" />
<p><em>Slika 2 Izlaz Atomic Red Team testa T1083 – File and Directory Discovery</em></p>
Rezultati testa pokazuju da ciljni sustav omogućuje širok uvid u strukturu datotečnog sustava bez dodatnih ograničenja. Iz perspektive napadača, ovakva razina pristupa omogućuje jednostavno lociranje konfiguracijskih datoteka, korisničkih direktorija ili drugih resursa koji mogu sadržavati osjetljive informacije. S obrambenog aspekta, nepostojanje detekcije ovakve aktivnosti predstavlja potencijalni sigurnosni nedostatak.

## Analiza Network Service Discovery i mrežnog skeniranja
Network Service Discovery testovi dopunjeni su ručnim mrežnim skeniranjem pomoću alata nmap. Na Slikama 3 i 4 prikazani su rezultati skeniranja interne mreže, uključujući identificirane aktivne hostove i dostupne mrežne servise.

<img width="605" height="454" alt="image" src="https://github.com/user-attachments/assets/b994085a-d31f-4c35-a958-b5817b3bf6bf" />
<p><em> Slika 3 Nmap skeniranje mreže – otkrivanje aktivnih hostova </em></p>

<img width="945" height="709" alt="image" src="https://github.com/user-attachments/assets/f4aa0545-0703-49db-b603-945fa2763f1b" />
<p><em> Slika 4 Nmap skeniranje – identificirani mrežni servisi </em></p>
Rezultati skeniranja pokazuju da su pojedini servisi dostupni unutar mreže, što napadaču omogućuje mapiranje mrežne topologije i identifikaciju potencijalnih ciljeva. Iako nisu svi portovi dostupni, sama mogućnost izvođenja skeniranja bez aktivne detekcije ukazuje na ograničenu vidljivost mrežnih aktivnosti unutar postojećeg sigurnosnog okruženja.

## Analiza Account Discovery i pokušaja pristupa
Tijekom faze otkrivanja korisničkih računa zabilježeni su pokušaji uspostave SSH veze prema ciljanim sustavima. Kao što je prikazano na Slici 5, pokušaji povezivanja rezultirali su porukom connection refused, što ukazuje na pravilno konfigurirana firewall pravila ili nedostupnost servisa.
 
## Neuspjeli pokušaji SSH povezivanja prema ciljnim sustavima

<img width="605" height="454" alt="image" src="https://github.com/user-attachments/assets/259a9fce-a2bc-4da3-8e35-e12d1507aa9d" />
<p><em> Slika 5 Neuspjeli pokušaji SSH povezivanja prema ciljnim sustavima </em></p>
Iako su pokušaji izravnog pristupa odbijeni, sama činjenica da napadač može testirati dostupnost servisa i korisničkih imena predstavlja potencijalnu prijetnju. Informacije prikupljene u ovoj fazi mogu se iskoristiti u kasnijim napadima, primjerice za brute-force napade ili ciljani socijalni inženjering.

## Analiza firewall logova (OPNsense)
Analiza zapisa vatrozida OPNsense prikazana je na Slikama 6 i 7. Log zapisi jasno prikazuju velik broj blokiranih pokušaja komunikacije između mrežnih segmenata, uključujući DNS, TCP i UDP promet.

<img width="945" height="591" alt="image" src="https://github.com/user-attachments/assets/26970553-d1da-45a5-b832-f68e57dacce3" />
 
<p><em> Slika 6 OPNsense firewall – blokirani mrežni promet (Live View) </em></p>

<img width="945" height="591" alt="image" src="https://github.com/user-attachments/assets/61a6795b-89c1-4464-bd37-e72adb14ce47" />
 
<p><em> Slika 7 Detaljni zapisi OPNsense vatrozida tijekom simuliranih napada </em></p>
Ovi zapisi potvrđuju da vatrozid učinkovito primjenjuje zadana pravila i sprječava neovlaštenu komunikaciju. Međutim, analiza također pokazuje da vatrozid funkcionira isključivo na razini mrežnih pravila, bez dublje korelacije događaja ili analize ponašanja, što ograničava mogućnost ranog prepoznavanja napadačkih obrazaca.

# Zaključak 
Na temelju provedenih Atomic Red Team testova i detaljne analize prikupljenih podataka može se zaključiti da implementirane osnovne sigurnosne kontrole, poput mrežne segmentacije i konfiguriranog vatrozida, pružaju početnu razinu zaštite informacijskog sustava. Vatrozid učinkovito ograničava neovlaštenu komunikaciju između mrežnih segmenata te sprječava izravne pokušaje pristupa osjetljivim servisima, što je vidljivo iz analiziranih log zapisa.
Međutim, rezultati testiranja jasno ukazuju na to da napadač, nakon ostvarivanja inicijalnog pristupa mreži, može uspješno provesti fazu otkrivanja informacija bez pravovremene detekcije. Testovi prikupljanja sistemskih informacija, pregleda datotečnog sustava i otkrivanja mrežnih servisa omogućili su napadaču stjecanje detaljnog uvida u konfiguraciju sustava i mrežnu topologiju, bez aktivnog upozorenja ili reakcije sigurnosnih mehanizama.
Takva razina vidljivosti napadačkih aktivnosti predstavlja značajan sigurnosni rizik jer prikupljene informacije mogu poslužiti kao temelj za daljnje, sofisticiranije faze napada, uključujući eskalaciju privilegija, lateralno kretanje unutar mreže i kompromitaciju dodatnih sustava. Nedostatak mehanizama za korelaciju događaja i ponašajnu analizu otežava prepoznavanje obrazaca koji bi mogli ukazivati na zlonamjernu aktivnost u ranoj fazi napada.
Zaključno, iako postojeće sigurnosne kontrole ispunjavaju osnovne zahtjeve zaštite, one nisu dovoljne za učinkovito otkrivanje naprednijih napadačkih tehnika. Ovi rezultati naglašavaju potrebu za implementacijom dodatnih sigurnosnih rješenja usmjerenih na detekciju, analizu i korelaciju događaja, što predstavlja temelj za izradu konkretnih preporuka za unaprjeđenje sigurnosti sustava u sljedećem poglavlju.
