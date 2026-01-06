# Finalno izvješće

Ovaj projekt bavi se primjenom alata Atomic Red Team za simulaciju kibernetičkih napada i procjenu vidljivosti napadačkih aktivnosti u kontroliranom virtualnom okruženju. Cilj projekta bio je demonstrirati kako se pojedine napadačke tehnike, temeljene na MITRE ATT&CK okviru, mogu reproducirati pomoću malih i ponovljivih testova te analizirati njihovi učinci na sigurnost informacijskog sustava.

U sklopu projekta izrađeno je virtualizirano mrežno okruženje koje simulira infrastrukturu organizacije s odvojenim LAN i DMZ segmentima. Kao središnji element mreže korišten je OPNsense vatrozid, koji ima ulogu kontrole i bilježenja mrežnog prometa između segmenata. Takva arhitektura omogućila je jasno praćenje komunikacije i analizu mrežnih tokova nastalih tijekom izvođenja napadačkih aktivnosti.

Napadačka strana realizirana je korištenjem operacijskog sustava Kali Linux i alata Atomic Red Team, koji omogućuje izvođenje pojedinačnih testova usmjerenih na konkretne napadačke tehnike. U ovom projektu fokus je stavljen na fazu otkrivanja informacija (discovery), uključujući prikupljanje sistemskih informacija, pregled datotečnog sustava, otkrivanje mrežnih servisa i osnovnu enumeraciju korisnika. Testovi su izvođeni pojedinačno kako bi se omogućila jasna analiza svakog scenarija.

Analizom rezultata utvrđeno je da mrežna segmentacija i pravilno konfiguriran vatrozid učinkovito ograničavaju izravne pokušaje neovlaštenog pristupa servisima te da se takvi pokušaji jasno bilježe u zapisima vatrozida. Istovremeno je pokazano da napadač, nakon inicijalnog pristupa mreži, može provoditi fazu otkrivanja informacija bez trenutne detekcije na razini sustava, čime stječe vrijedne informacije o konfiguraciji ciljanog okruženja.

Projekt je time uspješno demonstrirao praktičnu primjenu Atomic Red Team alata u svrhu sigurnosnog testiranja, naglašavajući važnost razumijevanja ranih faza napada i njihove uloge u pripremi složenijih napadačkih scenarija.

# Prijedlozi poboljšanja i budući razvoj

Iako projekt uspješno demonstrira osnovne principe simulacije napada i analize mrežnog prometa, rezultati ukazuju na potrebu za daljnjim unapređenjem sustava. Jedan od ključnih smjerova poboljšanja je proširenje postojećih sigurnosnih mehanizama sustavima koji omogućuju aktivniju detekciju i korelaciju događaja, osobito u ranim fazama napada poput otkrivanja informacija i ponašajne analize.

Dodatno, projekt je u trenutnoj fazi realiziran unutar lokalnog virtualnog okruženja, što predstavlja ograničenje u pogledu realističnosti mrežnih uvjeta. Kao budući razvoj predlaže se implementacija slične arhitekture u distribuiranijem okruženju, s većim brojem sustava i složenijim mrežnim topologijama, kako bi se omogućilo vjerodostojnije testiranje napadačkih tehnika i sigurnosnih kontrola.

Također, daljnji razvoj projekta mogao bi uključivati proširenje Atomic Red Team testova na dodatne MITRE ATT&CK taktike, poput eskalacije privilegija i lateralnog kretanja, čime bi se dobio potpuniji uvid u otpornost sustava na različite faze kibernetičkog napada. Na taj način projekt bi se mogao nadograditi iz demonstracijskog laboratorija u naprednije okruženje za kontinuirano sigurnosno testiranje i edukaciju.
