Mõiste – Operatsioonisüsteem – tarkvara, mis haldab, suhtleb kõigi riistvaraseadmetega madalal tasemel.

OS peamised ülesanded – Rakenduste progammeerimisliidese pakkumine, ressursside juhtimine

OpSys peidab ära riistvara kasutamise keerukuse, muud programmed saavad olla lihtsamad.

Käsurida pole osa operatsioonisüsteemist.

Haldab parallelseid protsesse (nt 4-tuumalisel protsessoril tuumade võimsuse jagamine programmide vahel)

Tänu OS-ile saavad programmid teha madala taseme tegevusi lihtsalt (nt failide loomine)

API – rakenduse progammeerimisliides (application programming interface). Viis, kuidas kaks või enam programmi saavad omavahel suhelda.

Madalatasemeline API – väga detailne, nt monitori piksli värvi ära muutmine. Graafikakaardi puhvrisse mingi jada kirjutamine.

Kõrgetasemeline API – rohkem spetsialiseerunud liides, muudab ressursside haldamise lihtsamaks, riistvara protsesside väljakutsumine. OS peidab madala taseme API kasutaja eest, sest selle UI on halva välimusega.

Kõvakettal pakub OS draivereid riistvara kontrollimiseks, faili abstraktsiooni, ilusat liidest failide haldamiseks, et lihtsustada nende lugemist, kirjutamist.

OS leiab, kus on vaba ruumi, mitmendale kihile kirjutada, kuhu sektorisse ja plokki, kuidas liigutada ketta lugemispead.

Fail – järjestatud ketta plokkide nimekiri. Failil on nimi ja asukoht failisüsteemis (teine abstaktsioon)

OS jätab meelde faili blokkide nimekirja ja nende asukohad. Vajadusel liigutab plokke ümber, et ketta ruumi optimeerida või vältida ketta korrupeeruvaid alasid.

Faili operatsioonid ilusas liideses – loomine, kirjutamine, lugemine, positsioneerimine (seek), kustutamine, pikkuse muutmine

OS pakub abstraktsiooni failide organiseerimiseks, nt kaustad, failide puu (algab juurkaustast).

OS jagab ressursse jooksvate programmide vahel (nt CPU, ketas, RAM), kirjutamise järjekord, võrgu läbilaskevõime.

Kontrollib kellel on õiguseid seadmeid kasutada või konkreetseid faile lugeda.

Kontekstivahetus (context switching) – mitu programmi pseudo- samaaegselt. Nt OS kernel; programmi käivitamiseks on vaja käivitada programmi kood ja OS protsessikood, mida tehakse vaheldumisi. Juhtvoo vahetumine.

OS-il on kihiline disain, kus allpool on madalatasemelised kõrgprivilegeeritud protsessid. Tuum (katkestused, protsesside juhtimine, mälu haldamine, turvalisus) -> draiverid/firmware -> üldteenused (sõnumite vahetamine, failisüsteemile ligipääs)-> rakendused.

OS kategooriad:

Sihtseadmete järgi – suurarvutid/serverid, PC-d, manustatud seadmed

Disaini keerukuse järgi – lihtsad (monoliitsed, koostööpõhised) ja keerukad (ennetav multitegumtöötlus, mitme kasutajaga)

Ajastus ja reageerimisvõime – reaalajasüsteemid, üldotstarbelised süsteemid.

Kerneli arhitektuur – monoliitsed, kihilised, mikrokernelid, hübriidid, eksokernelid

Jaotus ja skaleeritavus – ühe- ja mitmeprotsessorilised, hajutatud süsteemid, klasterdatud süsteemid.

Ajalugu – 19. Sajand, Charles Babbage. “Arvuti isa”. Difference engine. Analüütiline mootor (ALU, kontrollvoog, Mälu)

20. sajand –

1938 Z1, binaarsüsteem, piiratud programmeeritavus.

Z3 1941 – elektromehhaaniline, täisautomaatne. Telefoni kommunikatsiooniseadmed. Perforeeritud kilega programmeerimine. Esimene ujukomaarvude kasutus. Oli Turingi täielik (võimeline arvutama kõike, kui on piisavalt aega ja mälu)

Planalkül – esimene kõrgtasemeline programmeerimiskeel (Plan Calculus)

1950ndatel hakkas OS-I konseptsioon kujunema. Tööde järjestuse automatiseerimine, käsitsi sekkumise vähendamine.

IBM 701 SOAP (Symboli Optimal Assembly Program) – Esimesed katsed pakkuda automaatset järjestuse juhtimist. Kaubanduslikult saadaval.

GM- NAA I/O 1956 (General motors, N. Amrican Aviation) IBM 704 jaoks.

Üks esimesi, mis haldab pakett tööde I/O töötlust

Fortrani monitorisüsteem (FMS) – IBM 704 jaoks

CTSS – MIT-s töötatud, mitme arvuti koostöö, ajajagamissüsteem.

Multics – hierarhiline failisüsteem

UNIX (Thompson, Ritchie Bell Labsis) – Keskne tuum ehk kernel, unix shell käsurida, unix failisüsteem. Hiljem portiti C-keelele. Sellest arenes uus haru, mida tuntakse UNIX-laadsete süsteemide all. Aja jagamine ja multi-kasutaja funktsioonid.

CP/M – esimene personaalarvutite OS 70ndate lõpus.

BSD tutvustas uusi funktsioone Arvutivõrgu tugi ja TCP protokolli

DOS (Disk Operating System), MS-DOS muutus domineerivaks, IBM võttis PC-des kasutusele.

Mac OS sai tuntuks kasutajasõbraliku UI poolest.