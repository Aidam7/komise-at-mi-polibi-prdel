# 6 - Aktivní a pasivní síťové prvky, typy, parametry, konfigurace

## Aktivní prvky
- Aktivně se podílí na komunikaci v síti

### Opakovač - dnes se nepoužívá
- pracuje na první vrstě OSI modelu
- většinou má pouze dva porty
- slouží k prodloužení dosahu signálu, hlavně u sběrnicové topologie

### Hub - dnes se nepoužívá
- multipoint opakovač
- pracuje na první vrstvě OSI modelu
- 4 - 24 portů
- základní prvek pro hvězdicovou topologii

### Bridge - dnes se nepoživá
- pracuje na druhé vrstvě OSI modelu - rozhoduje podle MAC adresy
- většinou má pouze 2 porty
- slouží k propojení/oddělení segmentů
- snižuje velikost kolizní domény
- broadcasty a multicasty se posílají všude

### Switch
- multipoint bridge
- dělá vše, co bridge + navíc:
    - pracuje rychle 
    - základní prvek pro hvězdicovou topologii
    - nepravuje frame

- *princip funkce*
    - u přicházejících rámců čte zdrojovou MAC adresu a vytváří v paměti tabulku MAC adres a portů, odkud pochází, tabulka se označuje jako CAM (Content Addressable Memory) tabulka
    - pokud nemá pro cílovou MAC adresu záznam, tak rámec odešle na všechny porty mimo příchozího
    - pokud má v tabulce cílovou MAC adresu, tak rámec pošle pouze na daný port

#### Módy switche
Kvůli hledání kompromisu mezi zpožděním a spolehlivostí existuje několik metod.

> **Cut-Through** - rychlé, ale bez kontroly chyb, přeposílá framy okamžitě, kdy zná cílovou MAC adresu

> **Store-and-Forward** - nejprve se celý rámec přijme, ověří se frame check sequence a pak teprve posílá nebo zahodí

>**Fragment-Free (Modified Cut-Through)** - kompromis, nejprve načte prvních 64 bytů (včetně hlavičky) a pak přeposílá

### Router
- pracuje na třetí vrstvě OSI modelu (Layer 3) - rozhoduje podle IP adresy
- hraniční router se označuje jako gateway (brána)
- slouží pro spojování sítí
- nabízí služby uvnitř LAN (směrování ze zdroje do cíle, segmentování sítě, ARP) a propojení do WAN (přes serial, ISDN, DSL, optiku)
- broadcasty se standardně nepřeposílají - snižuje velikost broadcast domény
- je pomalejší než switch, často je dnes nahrazován Layer 3 switchem (MultiLayer Switch)
- vytváří novou hlavičku a ukončení (CRC) framu
    -  CRC je síťová metoda určená k detekci chyb v datech a informacích přenášených po síti

### Firewall

### Síťová karta (NIC)
- zprostředkovává komunikaci síťového zařízení se samotnou sítí
- každá síťová karta má svoji jedinečnou MAC adresu
- dělení: serverové x do běžných pracovních stanic

## Pasivní prvky
Nejdůležitější vlastnosti:
- Elektromagnetická odolnost
    - Odolnost vůči vnějším zdrojům energie
- Šířka pásma 
    - Rychlost přenosu dat
- Útlum
    - míra zeslabení signálu při průchodu kabelem
    - čím delší kabel, tím delší útlum
- Impedance
    - odpor, který kabel představuje pro připojené zařízení
    - impedance kabelu == impedance zařízení
- Zkreslení
    - odchýlení signálu, které vzniká při přenosu
    - čím delší kabel, tím větší zkreslení

<br>
<br>
<br>
<br>
<br>

![alt text](/Obrazky/diagram.png)

### Koaxiální kabel
- Tvořen dvěma soustřednými vodiči
- Základní části: vnitřní vodič, dielektrikum, foliové stínění, vnější vodič, vnější plášť
- Dva druhy: tlustý a tenký
- Výhody: jednoduchá instalace, vysoká EMS, využití pro přenos hlasu a videa
- Nevýhody: malá mechanická odolnost

### Kroucená dvojlinka
- Svazek /8/ vodičů spletených do páru
- Typy stínění: UTP, STP, FTP, S/STP
```
   ▪ nestíněná UTP (Unshielded Twisted Pair)
          • nestíněný kabel, velmi oblíbený
    ▪ stíněná STP (Shielded Twisted Pair)
         • stíněný kabel, větší odolnost vůči rušení
     ▪ stíněná FTP (Foiled Twisted Pair)
        • stíněná kroucená dvojlinka, stínění je kolem všech párů kabelu
```
- Výhody: snadné připojení, využití v telefonních rozvodech, snadná instalace
- Nevýhody: horší EMS, obtížnější práce s těžšími kabely

### Optický kabel
- Přenos světelných impulsů
- Druhy vláken: 
    - jednovidová 
        - velmi tenké jádro
        - světlo postupuje jen jednou cestou
        - velký útlum
        - rychlost až 50 GB/s
        - přenos až na 100 km
    - mnohavidová
        - tlustší
        - světelný paprsek má více prostoru => probíhá více cestami => může vést k rušení signálu
        - snáze se spojují
        - nejvyšší rychlosti do 1 km od vysílače
- Výhody: vysoká EMS, minimální útlum, bezpečnost
- Nevýhody: obtížné připojování, složitá montáž, vyšší cena

### Bezdrátové připojení
- Využívá se tam, kde není možné připojení drátem
- [více v otázce 9](/MaturitniOtazky/09%20-%20Bezdrátové%20technologie/README.md)
### Konektory a zásuvky
- Používají se pro propojení síťových médií s aktivními prvky
- Typy závisí na použité kabeláži: BNC pro koaxiální, RJ-45 pro kroucenou dvojlinku, různé typy pro optické kabely

![alt text](/Obrazky/kabely.png)