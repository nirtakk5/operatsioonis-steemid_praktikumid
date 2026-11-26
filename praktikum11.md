# XI praktikum: sissejuhatus võrgutehnoloogiasse
Selles praktikumis sain lisada VM-idele adaptereid, pingida IP-aadresse, rakendasin IP forwarding'ut. Mulle meeldis see praks väga, sest see ei olnud piinarikas. Võttis aega umbes 2h. 

11-1:
ruuter1:
-eth0: DHCP
-eth1: (staatiline IP) 192.168.28.1/24, võrgumask 255.255.255.0, võrguaadress 192.168.28.0, leviaadress 192.168.28.255

ruuter2:
-eth0: (staatiline IP) 192.168.28.2/24, võrgumask 255.255.255.0, võrguaadress 192.168.28.0, leviaadress 192.168.28.255
-eth1: (staatiline IP) 192.168.29.65/26, võrgumask 255.255.255.192, võrguaadress 192.168.29.64, leviaadress 192.168.29.127

klient:
eth0: (staatiline IP) 192.168.29.66/26, võrgumask 255.255.255.192, võrguaadress 192.168.29.64, leviaadress 192.168.29.127

<img width="959" height="565" alt="image" src="https://github.com/user-attachments/assets/915d31b7-d032-45c4-b063-259a75b0896d" />


11-2:

<img width="479" height="566" alt="image" src="https://github.com/user-attachments/assets/4000fa23-4ab7-459c-ac72-436a5934d779" />

Masinal ruuter2 on seadistatud ainult kaks sisevõrgu aadressi, mistõttu teab tema marsruutimistabel teed ainult nende kahe kohaliku alamvõrguni. Kuna me ei lisanud seadistusfaili gateway rida ega ole veel seadistanud staatilisi marsruute, ei oska ruuter2 saata pakette avalikku internetti (8.8.8.8) ja tuum katkestab päringu kohe veateatega


11-3:
Ilma NAT-ita (MASQUERADE) saadab ruuter1 paketid välisvõrku edasi nii, et nende lähteaadressiks jääb ruuter2 või klient privaatne sisevõrgu IP-aadress, mis pole avalikus internetis ega välistes lüüsides marsruuditav. Sihtserver (8.8.8.8) või vahepealne VirtualBoxi NAT-lüüs ei tea, kuhu vastuspaketid privaataadressile tagasi saata, mistõttu need visatakse minema. Kui ruuter1 peal aktiveeriti MASQUERADE, asendas ta väljuvate pakettide lähteaadressi oma välise liidese (eth0) IP-aadressiga, mistõttu jõudsid vastused tagasi ruuter1-ni ja sealt edasi õige sisevõrgu masinani.

11-4:

<img width="319" height="298" alt="image" src="https://github.com/user-attachments/assets/bd97f048-9ae3-41e7-ba7f-bdc03fac979d" />
