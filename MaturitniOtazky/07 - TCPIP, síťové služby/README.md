# 7 - TCP/IP, síťové služby a jejich konfigurace

## TCP/IP _(Transmission control protocol/internet protocol)_

1. Skupina protokolů umožňující komunikaci v počítačových sítí
2. Zařizuje směrování
3. Oproti modelu OSI má pouze 4 vrstvy a je více škálovatelný a využívá klient-server architekturu. Je lépe nasaditelný a tím se prosadil

### Vrstvy

1. Aplikační vrstva
    1. S touto vrstvou komunikují samotné aplikace, které potřebují přístup k internetu
    2. Různé protokoly (HTTP, adál)
2. Transportní vrstva
    1. Protokoly TCP a UDP pro komunikace
    2. TCP
        Lepší pro přímou komunikaci, různé funkce, např. obnovení, používané v situacích kdy je potřeba spolehlivá komunikace (email, prohlížení webu)  
        Větší hlavička (20-60B)  
        Segment  

- 1. UDP  
        Očekává, že příjemce dostane všechny packety, není velký problém když ne. Využíváno v situacích, kdy se více hodí vyšší rychlost, nižší latence (streamování videa, hraní her, ...)  
        Menší hlavička (8B)  
        Datagram
![TCP a UDP header](https://www.softwaretestinghelp.com/wp-content/qa/uploads/2020/02/header-TCP-vs-UDP.jpg)

- 1. Komunikuje přes Porty v aplikační vrstvě
        1. Každý port má přidělané číslo a vlastní specifickou funkci
        2. 80 – HTTP
        3. 20, 21 – FTP
        4. 22 – SSH
        5. 23 - TELNET
        6. 443 – HTTPS
        7. 25565 – MINECRAFT MULTIPLAYER DEFAULT PORT

(Více příkladů - [Structure of the Internet: Standard application layer protocols - Wikibooks, open books for an open world)](https://en.wikibooks.org/wiki/A-level_Computing/AQA/Paper_2/Fundamentals_of_communication_and_networking/Standard_application_layer_protocols)

- 1. Data od aplikační vrstvy protokol rozloží na mnoho balíčků - packety
  2. V hlavičce jsou instrukce jak balíčky opět složit do smysluplného výsledku a také kontrola, jestli příjemce vše dostal a správně složil

1. Internet
    1. Využívá IP (internet protocol) pro připojení Origin IP adresy a destination IP adresy k packetům
2. Network
    1. Vrstva Network spravuje zasílání na správné zařízení pomocí MAC Adres

## Služby (Přebráno a přeloženo z Bible – Jaroslav 16:4)

### DHCP (Dynamic Host Configuration Protocol)

- Porty 67 a 68 (67 Pro server, 68 pro klienta)
- Automaticky přiřazuje TCP/IP adresovací informace klientům)
- IP Adresu, masku, gateway, DNS, ...
- Využívá broadcast packety
- 4 Kroky
  - **Discover** – Klient pošle broadcast zprávu pro nalezení DHCP serveru
  - **Offer** – DHCP server nabídne IP adresu
  - **Request** – Klient příjme odpověď a zašle žádost o používání IP
  - **Acknowledge** – server alokuje IP adresu klientovi

### DNS (Domain name server)

- Port 53
- Využíván pro komunikaci mezi DNS serverem a klientem
- hierarchicky distribuovaná databáze
  - hierarchická (rozdělá do sobě nadřazených skupin - domény a subdomény)
  - distribuovaná (rozmístěna na více místech - name servery)
- jeho hlavnímí úkoly a příčinou vzniku jsou vzájemné převody doménových jmen a IP adres uzlů sítě
- např. ahoj.alexi.cz - nejprve se vyhledá skupina ‘.cz’, ve které se nalezne ‘.alexi’, ve které se nalezne ‘ahoj’ - toto se poté převede na IP

### Telnet

- Port 23
- umožňuje připojení ke vzdálenému počítači (absence šifrování dat, dnes nahrazen protokolem SSH)
- Terminal-to-terminal komunikace, variace různých užití (testování propojení)

### SSH

- Port 22
- Vyvinut jako náhrada pro Telnet a FTP
- kryptografický protokol, který umožňuje bezpečné připojení i přes nezabezpečenou síť
- Primárně používán jako bezpečná vzdálená administrace systému
- Klient pošle connection request serveru
- Po propojení se vyjednají různá informace (negoiate encryption alrogitmus, výměna kryptografického klíče, autentizace, ...)
- Po výměně server vyžádá auntentizaci uživatele
- Nastavena bezpečná terminal-to-terminal komunikace pro posílání příkazů na vzdálený server

### FTP (file transfer protocol)

- Port 20 a 21
- Protokol umožňující rychlý přenos dat mezi dvěma body (nejčastěji rp osdílení dat – hudba, videa)
- Možnosti nastavení uživatele
- Různé módy přenosu
  - Stream mode
  - Block mode
  - Compressed mode
- Nebezpečí při posílání hesel/zranitelných dat, jelikož se posílají jako plain text (FTPS, podporuje TLS - Transport Layer Security, větší odezva)

### HTTP (Hypertext transfer protocol)

- Port 80
- Využíván pro komunikaci s WWW servery na přenos hypertextových dokumentů (HTML, XML)
- Neumožňuje šifronání ani zabezpečení integrity dat, využívá se TLS, označováno jako HTTPS, Port 443)

### MMDP (Minecraft multiplayer default port)

- Port 25565
- Využíván hrou Minecraft pro vytvoření veřejného světa, umožní pozvání kamarádů na svět.

_Poštovní:_

### POP3

- Port 110
- Protokol pro stahování emailů ze vzdáleného serveru
- Nelze s emaily pracovat, pouze stahování, přečtení a mazání
- Všechny maily se stáhnou na zařízení, proto jde používat i offline

### IMAP

- Port 143
- Pro přijímání mailů přes mail client
- Umožňuje práci s maily
- Potřeba trvalé připojení
- Možnost více uživatelů

### SMTP

- Port 25
- slouží k odesílání elektronické pošty poštovním klientem (protokol zajišťuje doručení pošty pomocí přímého spojení mezi odesílatelem a adresátem)
- jeden z nejstarších protokolů určených pro elektronickou poštu

## **Porty**

- využívány především protokoly TCP a UDP - jednoznačně identifikují službu na zařízení, která komunikuje
- kladné 16bitové číslo
- celkový rozsah portů je 0-65535 (port 0 je rezervován pro odesílající proces - neočekává odpověď)
- porty jsou rozčleněny do třech skupin
  - dobře známé (1-1023, porty různých základních/známých protokolů)
  - registrované (1024-49151, porty přiřazené společností IANA specifickým službám)
  - dynamické/privátní (49152-65535, porty privátní pro identifikaci např. v lokální síti)
