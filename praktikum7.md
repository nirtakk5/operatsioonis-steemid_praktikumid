# VII Praktikum: Haakimine
Selles praktikumis sain mängida haakepunktidega. Mul juhtus mitu korda probleeme, aga sain lõpuks hakkama. Kokku läks umbes 5h?

7-1: 
1. Täiesti uuel või toorel kettal puudub partitsioonitabel (Partition Table, nt GPT või MBR). Lähtestamise käigus kirjutatakse ketta algusesse info selle kohta, kuidas ketas struktureeritakse. Ilma selleta ei tea operatsioonisüsteem, kust ketta ruum algab või lõppeb.
2. Windows ega ükski teine operatsioonisüsteem ei saa enne partitsioonide tegemist ja failisüsteemi (nt NTFS, EXT4, FAT32) vormindamist kettale faile salvestada. Lähtestamine on esimene kohustuslik samm enne uue lihtdraivi/partitsiooni loomist.
3. Lähtestamisel omistatakse kettale unikaalne identifikaator (GUID või ketta signatuur), mis võimaldab operatsioonisüsteemil seda ketast teistest eristada ja süsteemis õigesti hallata.

7-2:
1. GPT toetab kuni 9,4 ZB suuruseid kettaid ja partitsioone, samal ajal kui MBR piirdub maksimaalselt 2 TB-ga. MBR kasutab sektoriaadresside salvestamiseks 32-bitist väljahaagitud ruumi. Standardse 512-baidise sektori puhul on maksimaalne adresseeritav maht $2^{32} \times 512 \text{ bytes} \approx 2,19 \text{ TB}$. GPT kasutab aga 64-bitist adresseerimist, mis eemaldab praktikas ketta mahupüramiidi piirangud.
2. GPT toetab vaikimisi kuni 128 primaarset partitsiooni, ilma et peaks kasutama laiendatud partitsioone. Tehniline põhjendus: MBR-i partitsioonitabeli maht ketta alguses on piiratud 64 baidiga, millest piisab täpselt nelja 16-baidise partitsioonikirje jaoks. GPT eraldab partitsioonitabeli struktuurile tervelt 16 KiB ruumi, kus iga partitsioonikirje pikkus on 128 baiti.
3. GPT tuvastab partitsioonitabeli vigastused automaatselt ja suudab need taastada, samas kui MBR-i kahjustuse korral muutub kogu ketas loetamatuks. GPT kasutab tsüklilist koodkontrolli, et kontrollida nii GPT päise kui ka partitsioonitabeli terviklikkust igal käivitamisel. Kui süsteem tuvastab vea või andmete korruptsiooni, suudab see automaatselt taastada struktuuri ketta lõpus asuvast varukoopiast. MBR-il puudub igasugune kontrollsumma või varukoopia mehanism.
4. GPT dubleerib oma kriitilised struktuurid ketta viimastele sektoritele. MBR asub eranditult ainult ketta esimeses sektoris. Kui see üks sektor füüsiliselt kahjustub või üle kirjutatakse, kaob ligipääs kogu kettale. GPT kirjutab oma põhipäise ja tabeli ketta algusesse ning täpse koopia ketta viimastesse sektoritesse, tagades süsteemi töökindluse ka esimese sektori rikke korral.

7-3:
https://kodu.ut.ee/~katriinliivat/opsys/hdd.png

7-4:

<img width="285" height="56" alt="image" src="https://github.com/user-attachments/assets/c93c76fb-fc46-42a3-bec0-177116a76d5a" />

7-5:
-o ro: Määrab haakimisvaliku kirjutuskaitstuks. See tähendab, et haagitud mälupulgalt saab faile lugeda ja kopeerida, kuid sinna ei saa uusi faile salvestada, olemasolevaid muuta ega kustutada.
-t auto: Käsib operatsioonisüsteemil tuvastada failisüsteemi tüüp automaatselt. Kasutaja ei pea ise käsitsi täpset failisüsteemi tüüpi ette andma.

7-6:
Ubuntu asendas auto-parameetri väärtusega fuseblk

7-7:

<img width="297" height="260" alt="image" src="https://github.com/user-attachments/assets/82152310-90b4-4dac-827b-01fb2b3ba2bd" />
