Instalarea aplicațiilor în Debian GNU/Linux sau Ubuntu
======================================================

În general totul e construit pe filozofia UNIX *fă un singur lucru, dar fă-l bine*. Adică mai multe programe specializate pe domeniul lor, care comunică între ele, în locul unui mega-program care să facă tot.

`dpkg`
program pentru manipularea pachetelor .deb

este programul care se ocupă de instalarea efectivă a pachetelor (fișierele .deb) și este folosit de toate celelalte programe care „instalează/șterg” pachete[1].

Poate fi folosit pentru a instala fișiere .deb și pentru a afla informații despre pachetele instalate (respectiv fișierele lor). Necesită root pentru instalări/ștergeri dar poate fi folosit de orice utilizator pentru a obține informații. Nu este recomandat pentru instalare/ștergere decât în cazuri speciale.

Exemple[2]:

`# dpkg -i un_fișier.deb`

instalează fișierul .deb. Va eșua dacă nu sunt îndeplinite toate dependențele

`# dpkg -i pachet.deb dep1.deb dep2.deb`

instalează pachetele. dep1 și dep2 sunt dependențe pentru pachet (ordinea nu contează dacă sunt specificate toate odată, sau se instalează pe rând: mai întâi dependențele după care pachetul respectiv)

`$ dpkg -l`

afișează TOATE pachetele instalate sau care au fost vreodată instalate. Util pentru a vedea starea unui pachet: ii - totul ok.

`$ dpkg -l nume_pachet`
`$ dpkg -l nume_parțial*`
`$ dpkg -l *nume_parțial`
`$ dpkg -l *nume_parțial*`

afișează starea pachetelor instalat/șters/necunoscut/...

`$ dpkg -S nume_fișier`

afișează pachetul instalat care conține fișierul.

`$ man dpkg`

manualul de utilizare

`apt`
(scris și APT) - Advanced Package Tool

Este sistemul de gestionare a pachetelor. Pachetele pot proveni din diverse surse (CD, DVD, ftp, ...) enumerate în /etc/apt/sources.list sau în fișierele din /etc/apt/sources.list.d/

Pachetele sunt instalate conform următoarelor priorități:

 * prioritatea sursei
 * versiunea cea mai nouă a pachetului
 * ordinea listării sursei în sources.list

Prioritățile pot fi ajustate în /etc/apt/preferences (nu există implicit) sau prin opțiunea Default-Release din /etc/apt/apt.conf (nu există implicit).

Poate fi folosit prin intermediul programelor apt-get și apt-cache sau apelat ca „bibliotecă” de către alte programe.

`$ man apt`
`$ man apt.conf`
`$ man sources.list`
`$ man apt_preferences`

manualul pentru apt și fișierele de configurare

`apt-get`
program din pachetul apt (interfață pentru apt)

Poate fi folosit pentru instalare/ștergere de pachete. Considerat de nivel destul de jos, dar poate fi folosit pentru managementul sistemului. Necesită root pentru instalări/ștergeri, dar poate fi folosit de orice utilizator pentru descărcări de pachete, pachete-sursă.

Exemple:

`# apt-get update`

actualizeaza listele cu pachete (această comandă ar trebui să fie rulată întotdeauna înainte de a instala sau actualiza pachete)

`# apt-get upgrade`

actualizeaza toate pachetele care pot fi actualizate

`# apt-get install pidgin`

descarcă (dacă este necesar) pachetul pidgin, împreună cu toate dependențele și folosește dpkg pentru a le instala

`# apt-get purge pidgin`

șterge pachetul pidgin (inclusiv toate fișierele de configurare la nivel de sistem)

`# apt-get autoremove`

șterge toate pachetele care au fost instalate doar ca dependențe pentru alte pachete

`$ man apt-get`

manualul de utilizare

`apt-cache`
program din pachetul apt (interfață pentru apt)

Poate fi folosit pentru a obține informații despre pachete (instalate sau nu). Este mai rapid la căutări decât aptitude dar nu știe să caute decât în numele pachetelor sau descrieri.

Exemple:

`$ apt-cache search total commander`

toate pachetele care conțin total și commander în nume sau în descriere

`$ apt-cache search -n pidgin`

toate pachetele care conțin pidgin în denumire

`$ apt-cache policy`

afișează prioritățile surselor de pachete

`$ apt-cache policy pidgin`

afișează versiunile pachetului din toate sursele respectiv prioritatea și „versiunea candidată”, adică cea care va fi instalată implicit cu apt-get/aptitude/synaptic

`$ man apt-cache`

manualul de utilizare

`aptitude`
program pentru management de pachete și interfață pentru apt

aptitude folosește anumite funcții din apt, dar are implementat propriul rezolvator de dependențe (mai complex și mai puternic) și propria funcție de căutare. Pentru funcțiile de bază se poate spune că aptitude = apt-get + apt-cache dar fiecare implementează funcții pe care celelalte nu le au. Este recomandat față de apt-get de mai mulți ani, deși unii mai conservatori susțin că apt-get este mai bun.

aptitude are două moduri principale de lucru: linie de comandă și interactiv. Comenzile de bază sunt similare cu apt-get/apt-cache. În modul interactiv (text) folosește combinații de taste și meniuri. Există și o interfață grafică (gtk[1]), dar este încă în stadiu experimental.

Comenzile de bază sunt documentate în pagina man dar mult mai multă informație se găsește în fișierul /usr/share/doc/aptitude și în pachetul aptitude-doc-en.

`synaptic`
interfață grafică pentru apt (gtk)

Folosește direct apt (nu apt-get) pe post de „bibliotecă”. Este interfața grafică recomandată pentru apt, cel puțin până când aptitude-gtk va fi utilizabil.

`adept`
interfață grafică pentru apt (KDE)

A fost creat special pentru apt, dar n-a mai fost actualizat. De curând s-a fost demarat un proiect (Google Summer of Code) pentru a-l actualiza (adept 3.0). Există deja și o versiune beta, vrea cineva să testeze? :)

`kpackage`
interfață generică pentru management de pachete

Se pare că folosește comenzi apt-get în fundal (în loc să folosească direct apt) și nu implementează anumite funcții importante. NU este recomandat.

[1] în ghilimele pentru că toate acele programe apelează de fapt la dpkg

[2] # înseamnă că acea comanda necesită root, $ înseamnă că poate fi executată de orice utilizator

[3] gtk este toolkitul folosit de Gnome. Programele pot fi folosite fără probleme în KDE dar arată cam „deplasate” (grafică diferită). KDE folosește toolkitul qt.
Apare destul de des și terminologia „biblioteci gtk” față de „biblioteci gnome”. Distincția este subtilă, dar destul de importantă. Un program care folosește biblioteci gnome, respectiv kde probabil că folosește părți importante din mediul respectiv și e posibil să „tragă” multe dependențe (sau toată suita). Programele care folosesc doar bibliotecile gtk respectiv qt vor fi (mult) mai „ușoare”. 

[Autor: Andrei Popescu](http://yetanotherpersonal.blogspot.com/2009/06/despre-managementul-de-pachete-din.html)
