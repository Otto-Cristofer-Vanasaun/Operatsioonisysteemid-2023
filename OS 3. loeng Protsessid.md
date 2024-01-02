Teooriad on põhimõtted paremini OS maailmas navigeerimiseks :)

Programm - kirjutatud programmeerimiskeeles, mida muudetakse edasi arvutile mõistetavamaks. Salvestatakse arvutisse näiteks failina. Programmist saab protsess.
Protsess - arvuti loeb endale käsud sisse, täidab käske, kompileerib, interpreteerib. Protsessil on algus ja lõpp.
Protsessile kuulub
	Mälu - aadressi ala
	Protsessori aeg
	Protsessori staatus PCB-s
Programmist võib tekkida mitu protsessi.
Abstraktsel kujul programmi mõjutamisel on abiks programmeerimiskeeled. OS aitab programmi ja iseenda jooksmist kaitsta teiste eest.
Protsessi magasin, rekursioon, selle muutujad pannakse järgmisesse stacki.
Stacki suurus tavalisel 8MB, aga sõltub:
	protsesside arv
	OS piirangud (nt Linuxil ulimit)
	Programmi kompileerides Windowsil /STACK parameeter .exe faili luues
	C,C++ lipukestega
	Ära looda liiga palju OS poolt loodud pakutud stackile. Suurema andmemahu jaoks võiks kasutada Heapi.
Protsessi registrite arv määrab paralleelsete ja keerukate arvutuste limiidid.
Protsesside planeerimine
	võib joosta mitu samal ajal
	Ressursside jagamine mitme protsessi vahel
	ajajaotussüsteem, näiline paralleeltöötlus
	palju ressursse - mitu protsessorit (tuuma) jooksutavad mitut protsessi korraga
Protsessi tabelis on iga protsessi kohta mingisugune kogus infot iga konkreetse protsessi kohta. 
Protsesside planeerimiseks on palju erinevaid järjekordi
	Kõik protsessid
	Ready protsessid
	I/O taga ootavad protsessid
Protsesse liigutatakse järjekordade vahelt
Eri järjekordadel erinev haldus. Round-robin on kõige levinum.
Mõõdikud - load average, I/O wait (load average suht sitt, sest protsessi load ei pruugi olla stabiilselt sama)
Planeerijad
	Selekteeritavad
	mitteselekteeritavad
	Vahepealne saalib protsesse sisse ja välja
	Pikaajaline
		Uute protsesside loomine
		Hoolitseb multiprogrammeerimise astme eest
		käivitub harva
		õige protsessisegu hoidmine
	Lühiajaline
		Valmis protsesside hulgast valib sobiva
		kiire ja tihe töö
	
Erinevatel keskkondadele sobivad erinevad
	Batch
	Interactive
	Realtime

Protsessi lõpp
	Vabatahtlik (exit), kus vanemprogrammile antakse väljundinfo (0 - edukas, 1 - üldine viga, 126 - õiguste probleem).
	OS vabastab protsessiga seotud ressursid
	Sunniviisiliselt, vanem tapab (kill), OS tapab, admin tapab.
	Viimasel juhul tekivad zombi-protsessid. Echo käsuga saab alamprogrammide väljundit cache-st kontrollida.
	


Kontekstivahetus bad, protsesse vaja sisse ja välja laadida.
Lapsprotsessid
	Luuakse Fork käsuga
	Uus protsess on vanemale protsessile lapsprotsess
	Ressursse saab jagada või mitte. Näiteks protsessoriaja jagamine.

Puhverdamine
	Tootja toodab mingit infot ja tarbijaprotsess saab selle kätta ja kasutab seda.
	Infot on vaja puhverdada.
	Ühendusega seotud teadete järjekord.
	Olekud: null - mitte ühtegi teadet ei ole vahel, praktiliselt otsene suhtlus.
	Piiratud maht - etteantud arv teateid, kui saatmisel on järjekord täis, siis sünkroonne saatja blokeerub ruumi vabanemiseni UNIX PIPE


Protsessidevaheline side
	IPC - interprocess communication
	OS poolt pakutav mehhanism protsesside vahel side pidamiseks ja tegevuste sünkroniseerimiseks


Sünkroniseerimine
	Teadete saatmine võib olla blokeeruv või mitte.
	Blokeerumine annab sünkroonse suhtluse
	Mitteblokeerumine annab asünkroonse suhtluse.
	Saatmine ja vastuvõtt võivad olla teineteisest sõltumatult blokeeruvad või mitteblokeeruvad.


Otsene suhtlus
	Protsessid peavad teadma teise protsessi nime nii saatmiseks kui vastuvõtmiseks. Näiteks P2P, Teams, Mänguklient ja server
	Sidekanali omadused
		Ühendused on automaatsed
		Seotud täpselt ühe paari protsessidega.
		Ühendus võib olla ühesuunaline, enamasti on kahesuunaline.

Kaudne suhtlus
	Teated postkasti, sealt võetakse ka vastu.
	Igal postkastil oma ID
	Suhtlus vaid siis, kui postkasti jagatakse.
	Ühendus võib olla paljude protsesside vahel
	Võib kuuluda nii rakendusele kui OS-ile.
	Analoogne portile.
	Postkastil on omanik, saab reguleerida, kellelt andmeid vastu võtta.
	Näiteks Mach, Windows 2000


Klient-server
	Sokkel on side otspunkt
	Side on kahe sokli puhul, nt IPv4

