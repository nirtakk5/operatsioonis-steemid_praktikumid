# X praktikum: ressursihaldus
Selles praktikumis sain tuttavaks arvuti programmide CPU ja mälukasutuse kontrollimisega. VM crashis sha1sum käskude peale mitu korda. Kokku läks aega 3,5 h , aga see oli väga piinarikas. 

|ülesanne|Linux|Windows|Linuxis kasutatud käsklus|Windowsis kasutatud tööriist ja väli|
|---|---|---|---|---|
|10-1|239|353|"ps -e --no-headers | wc -l"|tegumihaldur, jõudlus, CPU|
|10-2|systemd|smss.exe|"ps -eo pid,comm,lstart --sort=start_time | head -n 5"|process explorer, process|
|10-3|avahi, _chrony, cups-browsed, katriin, messagebus, polkitd, root, rtkit, syslog, systemd-oom, systemd-resolve|katriinliivat, DWM-1, LOCAL SERVICE, NETWORK SERVICE, SYSTEM, UMFD-0, UMFD-1|"ps -eo user --no-headers | sort -u"|tegumihaldur, üksikasjad, kasutajanimi|
|10-4|42 minutit|10:16:23:22 (ma lasen oma arvutil peale seda puhata)|"uptime -p"|tegumihaldur, jõudlus, tööaeg|
|10-5|5296 kworker/0:1-eve Mon Nov 23 18:12:32 2026|msedge.exe|"ps -eo pid,comm,lstart --sort=start_time | tail -n 5"|tegumihaldur, start time|
|10-6|Xorg (2,2%)|VirtualBoxVM(24%)|"ps -eo pcpu,pid,comm --sort=-pcpu | head -n 5"|tegumihaldur, üksikasjad, CPU|
|10-7|snapd(1907140 kB)|msedge(3891091488 kB)|"ps -eo vsz,pid,comm --sort=-vsz | head -n 5"|process explorer, Virtual size|
|10-8|nextcloud (270080 kB)|VirtualBoxVM.exe (4343600 kB)|"ps -eo rss,pid,comm --sort=-rss | head -n 5"|tegumihaldur, üksikasjad, Töökomplekt(mälu)|
|10-9|29,3% used 994 MB, 5,95% free 202 MB|78% kasutatud 24.5 GB, 20% saadaval 6,9GB|"free -m"|tegumihaldur, mälu|
|10-10|Avail = 8G, protsent = 34|vabaruumi 183 GB ehk 38,4%|"df -h /"|failihaldur, See arvuti, (C:), atribuudid|
|10-11|fail="swap.img"(3.6G), kaust="usr"(7.6G)|fail on üks OS-Liivat-W11 snapshot (40.88 GiB), kaust="Users"(172.59 GiB)|"sudo find / -xdev -type f -exec du -h {} + 2>/dev/null | sort -rh | head -n 5" ja "sudo du -h -d 2 / 2>/dev/null | sort -rh | head -n 10"|WinDirStat, (C:), füüsiline suurus|
|10-12|Kummagi käsu puhul kulub aktiivsest protsessoriajast enim aega sy tegevusele. /dev/zero puhul oli 55.6% sy (ja 22.2% us) ning /dev/urandom puhul 29.5% sy (ja 8.2% us, ülejäänud 62.0% id tuleneb vabadest protsessorituumadest)|   |"sha1sum /dev/zero | sha1sum /dev/zero" ja "sha1sum /dev/urandom | sha1sum /dev/urandom"|   |
|10-13|   |10-13-1:VirtualBoxVMN.exe, 10-13-2:C:\Users\katriinliivat\Documents\VirtualBox VMs\OS-katriin-Ubuntu26\Snapshots, 10-13-3:msedge.exe, 10-13-4: C:\Users\katriinliivat\AppData\Local\Microsoft\Edge\User Data\Default\Storage|   |   |
|10-14|   |Local Address=192.168.6.202, Local Port=61352, Remote Address=16.15.253.158, Remote Port=443, Latency (ms)=133, Total (B/sec)=83490|   |resource monitor, network|

10-12 pildid:
sha1sum /dev/zero | sha1sum /dev/zero:

<img width="1271" height="891" alt="image" src="https://github.com/user-attachments/assets/d177784c-b496-48e1-af45-f5024fa26b44" />

sha1sum /dev/urandom | sha1sum /dev/urandom:

<img width="1280" height="897" alt="image" src="https://github.com/user-attachments/assets/091431ef-4bc0-4069-a1ed-5637d149b808" />


10-13:
  10-13-1:
  VirtualBoxVMN.exe
  10-13-2:
  C:\Users\katriinliivat\Documents\VirtualBox VMs\OS-katriin-Ubuntu26\Snapshots
  10-13-3:
  msedge.exe
  10-13-4:
  C:\Users\katriinliivat\AppData\Local\Microsoft\Edge\User Data\Default\Storage


10-14 pilt:

<img width="785" height="440" alt="image" src="https://github.com/user-attachments/assets/804aece3-6f05-4bfc-b571-69352823317b" />

10-15:
Avan Task Manageri (Ctrl+Shift+Esc) -> vahekaart Performance ja Processes.
Kontrollin esmalt CPU kasutust (kas mõni protsess võtab püsivalt üle 80–90% CPU-d), seejärel Memory kasutust (kas RAM on täis >90% ja süsteem kasutab aeglast saalemälu/Pagefile'i) ning Disk vahekaardil Active time näitajat (kas ketas on 100% hõivatud ja keskmine reageerimisaeg Average response time on üle 50–100 ms).
Täpsema ketta- või võrgukoormuse tekitaja leidmiseks avan Resource Monitori (resmon) ning sorteerin Disk vahekaardil protsessid veeru Total (B/sec) järgi.
