Linuxi määratlus
	Avatud lähtekoodiga, väga kohandatav, kaasaskantav.
	kernel.org
	Termin "Linux" viitab tehniliselt ainult kernelile, kasutatakse seda tavaliselt kogu Linuxi tuuma ümber ehitatud süsteemi kirjeldamiseks. Paljud komponendid pärinevad GNU projektist.

Linuxi riistvara
	Sai kohendatud töötama serverite, PC-de, mobiilide, manussüsteemide OS-ina.

Perekonnad
	Debian ja selle tuletised
		Ubuntu, Mint, Kali
	Red hat
		Fedora
	SUSE, Arch Linux, Slackware, Gentoo.
	Android, OpenWrt, Yocto
	Edubuntu, Amazon Linux, SystemRescue, SteamOS

Kihiline OS - OS-i välimisi kihte saab kergemini vahetada.
/ ja : (Windowsis \ ja ;)
Linus Torvalds, Minixi inspiratsioon (mini UNIX, Tanenbaumi loodud Edu OS).
Richard Stallmani GNU ei ole UNIX. Linuxi tuuma ja GNU tööriistadega töötas välja täieliku OS-i.
Algselt ei vastutatud ametlikult koodi eest, Red Hat oli esimene kommertsprodukt.
2004 Ubuntu esimene versioon
2003 Android Inc
Linuxist sai pilveandmetöötluse standard. Docker, Linuxi konteinerid. Microsofti Windowsi alamsüsteem Linuxile (WSL).
Komponendid
	Kernel on põhikomponent. Vastutab arvuti riistvaraga liidestamise ja tarkvarale teenuse osutamise eest. Protsesside loomine, mäluhaldus, liidesed riistvaraga. Turvalisus, isoleerib rakendusi. Monoliit - suurem osa selle funktsioonidest on integreeritud kerneli ruumi. Toetab laaditavaid mooduleid.
	Kest (shell) - kasutajaliides, kasutajate suhtluskanal tuuma ja utiliitidega. Käsurida või graafiline.  Bash, Shell, töölauakeskkonnad. Tõlgendab käske kasutajalt. Skriptimisvõimalused, kasutajate ülesannete automatiseerimine. Haldab muutujaid ja seansse.
	Utiliidid - OSi tööriistad. Põhiläsud nagu ls (kataloogi sisu loeng), cp, mv. Tekstitöötlus nagu grep, awk, sed. Võrgundus nagu ifconfig, ip, netstat.


Failisüsteemi puu
	bin - olulised kasutajakäsud
	boot - käivitusfailid
	dev - seadmefailid
	etc - sysconfig failid (õigused jne)
	home - kasutaja koduhuinja
	lib - jagatud teegid, kernelivärk
	media - mount point eemaldatavale meediale
	mnt - mount point ajutistele failisüsteemidele
	opt - add-on tarkvara pakid
	sbin - süsteemi binaaaaaaaaaaaaaaaaaaaar
	srv - teenuste andmed tulevad siit
	tmp - ajutised failid
	usr -
	var - muutujafailid
	root - juurkasutaja home

Failide ja kataloogide omandi haldamine
	-l pikk formaat
	-h inimestele loetavad suurused
	chown uus_omanik failinimi
	-R rekursiivselt (iga kataloogi iga fail)
	chgrp vaheta gruppi
	omaniku, grupi õigused ja muud load
	rwx 421
	chmod
	u - omanik
	g - rühm
	o - teised
	a - kõik
	+-= (lisa, eemalda, lisa see ja eemalda teised)
	kataloogil rwx - sisu loetlemine ja failide võtmine, failide ja alamkategooriate loomise/kustutamise luba, sisenemise luba (cd)
	u+s u-S chmod setuid (binaarfailid ja skriptid). Määratakse protsessi käivitamisel protsessi omanik. Setgid teeb sama grupiga.
	
