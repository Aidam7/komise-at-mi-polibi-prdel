Fuse = FILE SYSTEM IN USERSPACE

vznikl, aby mohly byt vytvareny souborove systemy v uzivatelskem prostoru
implementovan na stejne urovni jako ostatni FS, tedy pod VFS
FUSE jaderny modul ale vystavuje API do userspace pres libfuse

Libovolna aplikace muze pristupovat k datum ruzneho druhu za vyuziti VFS
	Jako s souborum jinuch souborovych systemu
	Na druhem konci neni ovladac FS v jadre, ale uzivatelsky program, ktery poskutuje jadru pristup do daneho FS

Dopady implementace FUSE
	Jednoduchost implementace FS
	vice moznosti pro neprivilegovane uzivatele
	vetsi stabilitu a bezpectnost systemu
	moznost implementace v libovolnem jazyce
	moznost pouzit implemetnaci nekompatibilni s GPL

adbfs - pripojeni android telefonu pres USB
gitfs - FS integroanvay s GIT
xmlfs - XML soubor


procfs - virtualni souborovy system
	poskytuje informace o bezicich procesech
	musi byt standardne zakompilovan do jadra a pripojen na /proc
		na korenove urovni /proc ve VFS obsahuje jeden adresar pro kazdy bezici proces s nazvem PID procesu
		Symbolicky odkaz self odkazuje na adresar aktualniho procesu
		U vicevlaknovych procesu lze zjisti informace o jednotlivych vlaknech

attr - atributy bezpecnosti techologie SELinux
cwd  - symbolicky odkaz na aktualni pracovni adresar procesu


Roura
jde o metodu mistni komunikace mezi procesu
jedna se o:
	anonymni roury, 
	pojmenovane roury, 
	komunikace pomoci zprav

pojmenovana roura {named pipe, fronta FIFO} - komunikacni objekt pouzivany podobne jako nepojmenovana roura
pojmenovana roura prebyva ve svem domovskem adresari i v dobe, kdy s ni zadny proces nepracuje
muze byt tedy ulozena do archivu a nasledne obnovena - jde vlastne o specialni soubor
pred vyuzitim pojmenovane roury se musi vytvorit k tomu vyuzijeme volani mkfifo()
jako argument vyuziva cestu v souborov :{

roury jsou objekty orientovane na proud bajtu - nestrukturovana data
potrebujeme li prenaser zpravy o pevne danem formatu vyuzijeme technologii urcenou pro tuto oblast, napr: psosi messae queues, mQTT, rest api
technologie specifikovana primo na posix
vyzaduje podporu jadra, prislusnou knihovnou pro uzivtaleske programy
technologie posiq pmq umoznuje vytvaret pojmenovane fronty
do teze fronty muze proces zpravy posilat a odebirat
notifikace pri prochodu zpravy muze byt asynchronni nebo synchronni



sockety
jedna se o komunikaci metodu pouzivanu jak pres pociacovou sit tak i mistne
vyhoda spociva hlavne v transparentnosti vuci transportni vrstve
pro praci se sockety je vuyizvano rozhrani Berkeley sockets
sotcket - datovy objekt obsahujici informace o stavu komunikace s druhou stranou
pro vlastni komunikaci pouzivame systemova volani, ktera na dany objekt odkazuji deskriptorem

druhy prenisu socketove komunikace
spojovy {proudovy, streamovy} {TCP}
	nejdrive je sestaven komunikacni kanal, na ktery se nasledne zasilaji data v podobe produu bajtu
datagramovy {UDP}
	sestaven balik dat - datagram - ktery je odeslan jako celek

nejcasteji pouzivany typ komunikace
nemusi resit delku paketu, neresime spolehlivost prenosu

spojeni na strane klienta:
vytvoreni soketu
pripadne prirazeni nazvu (ip adresa a cislo portu)
pripojeni na server (vytvoreni komunikacniho kanalu)
vlastni komunikace
odpojenu od serveru
zruseni soketu

komunikace na strane serveru:
vytvoreni socketu
prirazeni nazvu
nastaveni socketu na "naslouchaci rezim"
cekani na pripojeni klienta
komunikace s klientem
ukonceni spojeni
zavreni socketu


obsluha vsech klientu v tomtez {jedinem} vlakne jako cekani na dalsi klienty
obsluha jednotlivych klientu v samostatnych procesech
obsluha jednotlivych klientu v samostatnych vlaknech
ruzne kombinace predchozich moznosti

hlavni rozdil v priprave na komunikaci:
sockety - sitove orientovane zalezitosti
roury - ryze mistni

sockety volime tam, kde se pocita se sitovou transparenci

bezpecnost:
roury - klasicka prava pro pristup k soouborum
sockety - pro mistni sockety ano
pro sitove sockety reseni na urovni aplikace nebo paketoveho filtru v jadre
