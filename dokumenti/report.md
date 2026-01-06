# Finalno izvješće

Ovaj projekt bavi se dizajnom i implementacijom sigurnosnog laboratorijskog okruženja za simulaciju i detekciju kibernetičkih napada korištenjem Atomic Red Team metodologije. Cilj projekta bio je uspostaviti realističnu, segmentiranu mrežnu infrastrukturu te demonstrirati suradnju napadačke i obrambene strane kroz simulirane napade i analizu sigurnosnih detekcija, uz jasno razdvajanje uloga Red Team i Security Analyst.

U sklopu projekta implementirano je virtualizirano mrežno okruženje koje se sastoji od firewall sustava, radnih stanica u LAN segmentu, serverskog sustava u DMZ zoni te napadačkog sustava. Kao središnja sigurnosna komponenta korišten je OPNsense firewall, koji omogućuje segmentaciju mreže, kontrolu prometa i implementaciju sigurnosnih pravila između LAN i DMZ mreža. Takva arhitektura omogućava realističnu simulaciju mreže kakva se može pronaći u stvarnim organizacijama.

Poseban naglasak stavljen je na sigurnosno ojačavanje (hardening) firewall konfiguracije primjenom principa minimalnih privilegija i politike default deny. Umjesto generičkih pravila koja dopuštaju sav promet, definirana su precizna pravila koja omogućuju samo nužne servise između mrežnih segmenata, dok je sav ostali promet blokiran i evidentiran. Time je smanjena površina napada i omogućena jasna vidljivost potencijalno zlonamjernih aktivnosti.

Kao ključna obrambena komponenta implementiran je Intrusion Detection System (IDS) temeljen na alatu Suricata, konfiguriran u monitoring modu. IDS sustav nadzire promet na LAN i DMZ sučeljima te koristi Emerging Threats Open rulesete za detekciju sumnjivih aktivnosti poput mrežnog izviđanja, pokušaja eksploatacije i zlonamjerne komunikacije. Ovakav pristup omogućuje detekciju napada bez aktivnog blokiranja prometa, što je prikladno za edukativni i analitički kontekst projekta.

Napadačka faza projekta provedena je korištenjem Atomic Red Team testova, koji se temelje na MITRE ATT&CK okviru. Atomic Red Team omogućuje izvođenje malih, kontroliranih testova koji simuliraju stvarne taktike i tehnike napadača, poput izviđanja sustava, pokušaja neovlaštenog pristupa i zlonamjernog ponašanja. Time se omogućuje sustavno testiranje sposobnosti detekcije sigurnosnih kontrola bez nanošenja stvarne štete sustavu.

Uloga Security Analysta bila je usmjerena na praćenje IDS alerta i firewall logova tijekom izvođenja napadačkih testova, analizu detektiranih događaja te procjenu učinkovitosti postojećih sigurnosnih mjera. Rezultati su pokazali da pravilno konfiguriran firewall u kombinaciji s IDS sustavom omogućuje pravovremenu detekciju velikog broja simuliranih napada, posebno onih povezanih s mrežnim skeniranjem i sumnjivim komunikacijskim obrascima.

Projekt je rezultirao funkcionalnim sigurnosnim laboratorijem koji demonstrira kako se open-source alati mogu koristiti za praktično učenje kibernetičke sigurnosti, testiranje otpornosti sustava i razumijevanje odnosa između napadačkih i obrambenih tehnika. Implementirano rješenje jasno prikazuje važnost segmentacije mreže, pravilnog hardeninga sustava te kontinuiranog nadzora i analize sigurnosnih događaja, što su ključni elementi suvremenih sigurnosnih operacija.

# Prijedlozi poboljšanja i budući razvoj

Iako implementirano rješenje ispunjava ciljeve projekta, postoji prostor za daljnja poboljšanja. Jedan od mogućih smjerova razvoja je proširenje obrambenog dijela sustava uvođenjem SIEM rješenja, čime bi se omogućila centralizirana korelacija logova, naprednija analiza događaja i dugoročno pohranjivanje sigurnosnih zapisa. Time bi se dodatno povećala vidljivost i mogućnost forenzičke analize napada.

Dodatno, projekt je u trenutnoj fazi realiziran unutar lokalnog virtualiziranog okruženja. Kao buduće poboljšanje predlaže se implementacija slične arhitekture u distribuiranijem ili realnijem okruženju, primjerice korištenjem više fizičkih ili virtualnih hostova povezanih putem stvarne mreže. Takav pristup omogućio bi vjerodostojnije testiranje mrežnih napada, latencije i sigurnosnih mehanizama u uvjetima bližima produkcijskom okruženju.

Također, daljnji razvoj mogao bi uključivati proširenje Atomic Red Team testova na veći broj MITRE ATT&CK taktika te usporedbu detekcijskih mogućnosti različitih IDS i IPS rješenja. Time bi se dodatno produbilo razumijevanje ograničenja i prednosti pojedinih sigurnosnih alata u suvremenim obrambenim sustavima.
