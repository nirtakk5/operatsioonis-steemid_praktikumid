# VI praktikum: Failiõigused Linuxis
Selles praktikumis sain katsetada failiõiguste seadistamist Linuxis. Sain teha gruppe ja grupisiseste liikmete õigustega mängida. Vahepeal lakkas terminal töötamast, aga sain ikkagi korda. Kokku läks umbes 2h. 

6-1:
a) Kataloogi sisenemiseks ja selle sees oleva faili teeni jõudmiseks on vajalik täitmisõigus (x). Faili enda sisu vaatamiseks ja lugemiseks on vaja lugemisõigust (r).
b) Unixis tähendab faili kustutamine kataloogi sisukorra muutmist. Seetõttu on vaja kataloogis kirjutamisõigust (w) ja sinna sisenemise õigust (x). Faili kustutamiseks ei ole vaja failil endal ühtegi õigust (r, w ega x), sest muudatus tehakse kataloogi, mitte faili enda sisu tasemel.

6-2:
Kesta/shelli-skript (.sh) ei ole kompileeritud masinkood ehk binaarfail, vaid tavaline tekstifail, mis sisaldab rearea-haaval täidetavaid käske. Ei piisa ainult käivitusõigusest (x), sest kesta-interpretaator ei saa faili sisu ilma lugemisõiguseta kätte. Lisaks käivitusõigusele (x) on kindlasti vaja ka lugemisõigust (r), muidu interpretaator ei saa faili lugeda.

6-3:
Kasutaja privaatgrupp (UPG):
Igal kasutajal on täiesti oma grupipõhine "saar". Kui kasutaja tekitab uue faili, saab selle faili omanik-grupiks tema isiklik privaatgrupp, millesse vaikimisi ei kuulu ükski teine kasutaja.
umask 0002 lubab grupil faili muuta ja kirjutada, aga kaasa antud privaatgrupis on ainult kasutaja ise, mistõttu on fail siiski teiste süsteemi kasutajate eest kaitstud (teistele ehk others kehtib 0002 tõttu vaid lugemisõigus r--)
Turvalisus: Kasutaja saab luua faile muretsemata, et mõni teine samas üldises grupis (nt users) olev kasutaja saaks tema faile muuta.
Kui on vaja teha teise kasutajaga koostööd, lisatakse mõlemad kasutajad eraldi ühisesse projekti-gruppi ning muudetakse kausta või faili gruppi (chgrp). Tänu umask 0002-le saavad nüüd mõlemad projekti liikmed faile vabalt muuta, ilma et peaks iga kord õigusi manuaalselt chmod-iga avama.

6-4:

<img width="374" height="134" alt="image" src="https://github.com/user-attachments/assets/a4c5526e-b360-4199-8e5f-bcabd276ac64" />

6-5:

<img width="350" height="69" alt="image" src="https://github.com/user-attachments/assets/bd43b4d8-eb67-4dd0-abff-d8011b99aa00" />

setuid võimaldab tavakasutajal käivitada programmi selle omaniku õigustes. Seda on vaja olukordades, kus tavakasutajal on vaja teha spetsiifilist toimingut, mis nõuab kõrgemaid privileege, ilma et kasutajale tuleks anda otsest ligipääsu kaitstud failidele või süsteemi admin-õigusi.

6-6:
Tõstab turvalisust (kui probleemi lahendust): See võimaldab järgida minimaalsete privileegide põhimõtet – kasutajale antakse piiratud ligipääs ainult ühele konkreetsele rakendusele/funktsioonile (nt parooli muutmine või hinne lugemine), andmata talle üldist õigust lugeda konfidentsiaalseid faile või administraatori õigusi.
Vähendab turvalisust (turvariskid): Kui setuid-iga märgistatud programm sisaldab turvaauku (nt sisendi kontrolli puudumine või mälu ületäitumine), saab ründaja seda ära kasutada, et käivitada oma koodi programmi omaniku (või root-i) õigustes, mis viib süsteemi üle võtmiseni. 

6-7:
1. peeter – faili enda omanik.
2. opetaja – kataloogi /tmp/yhiskaust omanik.
3. root – süsteemi superkasutaja (administraator).

6-8:
Õiguste reas ilmub tavapäraste õiguste lõppu pluss, näiteks -rw-rw-r--+. Pluss tähistab, et failile on rakendatud laiendatud juurdepääsuloend ehk ACL.

# file: hinded.txt
# owner: opetaja
# group: opetaja
user::rw-
group::---
group:direktor:rw-
mask::rw-
other::---

6-9:
1. Mitte keegi (isegi mitte root ehk administraator) ei saa faili sisu muuta, sellele juurde kirjutada, seda ümber nimetada ega kustutada seni, kuni +i atribuut on peal.
2. "sudo chattr -i testfail-2" ja siis "rm testfail-2"
