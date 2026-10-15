# Praktikum V: Protsessid ja signaalid
Selles praktikumis sain katsetada erinevaid signaale ja käske linuxi käsureal. Õppisin ka kuidas käske käivitada taustal ning neid ühendada torudega. Selle praktikumi peale kulus umbes 4h? 

Ülesanne 5-1:
<img width="566" height="94" alt="ül5-1" src="https://github.com/user-attachments/assets/b8e2e15a-7961-4ec9-a4bc-21c56041c7df" />

Ülesanne 5-2:
<img width="618" height="257" alt="ül5-2" src="https://github.com/user-attachments/assets/dbcfc3d2-9f07-4b6e-b230-53320c7062ba" />

Ülesanne 5-3:
<img width="636" height="140" alt="ül5-3" src="https://github.com/user-attachments/assets/8226c759-5cf4-4a71-bf8e-27dfe46b7314" />

Ülesanne 5-4:
ip a | grep "inet "| grep -v "127.0.0.1" | tr -s ' ' | cut -d ' ' -f 3 | cut -d '/' -f 1 > ipaddress.txt
Ülesanne 5-5:

"WM_SETCURSOR",787196,33554433 - Saadetakse aknale kui hiir liigutab hiireosutit aknas ja hiire sisendit ei saadeta. 
wParam - Aken, kus kursor asub, viide
lParam - lParam madalama järgu sõna määrab kursoripositsiooni tabamise testi tulemuse. Võimalike väärtuste jaoks vaata WM_NCHITTEST tagastatavaid väärtusi. lParam kõrgema järgu sõna määrab hiire aknasõnumi, mis selle sündmuse vallandas, näiteks WM_MOUSEMOVE. Kui aken siseneb menüürežiimi, on see väärtus null.

"WM_MOUSEMOVE",0,11796685 - Postitatakse aknale, kui hiir liigub. Kui hiirt ei tuvastata, postitatakse sõnum sellesse aknasse, kus on hiireosuti. Muidu postitatakse sõnum aknasse, mis tabas hiire.
wParam - Näitab, kas erinevad virtuaalvõtmed on all. See parameeter võib olla üks või mitu järgmistest väärtustest.
lParam - Madalord sõna määrab kursoris x-koordinaadi. Koordinaat on suhteline kliendi ala ülemise vasaku nurgaga. Kõrgeord sõna määrab kursoris y-koordinaadi. Koordinaat on suhteline kliendi ala ülemise vasaku nurgaga.

21:48:15.811,522,"???",4294377472,8191565 
<img width="510" height="112" alt="ül5-4" src="https://github.com/user-attachments/assets/e4348bd0-05f6-4d96-bcc7-3535d044c000" />
