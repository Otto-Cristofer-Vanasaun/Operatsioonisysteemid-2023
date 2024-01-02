Igal protsessil on registrid.
Registrite seis näitab protsessi täitmise järge. Seal kuskil on ka stack pointer.
Mitmelõimelisel protsessil on mitu registrite hulka, mitu stack pointerit, mitu täitmisjärge. Protsessor jooksutab ühes protsessis mitut üksust korraga.
Mitmelõimelisusega tuleb arvestada, koodi kirjutamise ja haldamise aeg läheb raskemaks, sest programmil on kindel järjekord, aga eri lõimed ei pruugi õigeid etappe õigel ajal valmis jõuda.
Põhjused:
	Võrreldes ühelõimelise protsessiga:
	Suurem reageerimiskiirus, parem interaktiivsus.
	Võimalus kasutada mitut protsessorit ühe protsessi jaoks.
	Võrreldes mitme eri protsessiga
	Ressursside jagamine - aadressipiirkond on mitme täitja poolt kastutatav
	Hoitakse kokku jagatud ressursside, uute protsesside loomise ja kontekstivahetuse pealt.
Kasutajataseme lõimed
	Realiseeritakse kasutaja tasemel teegina.
	Tuum ei tea midagi, tema jaoks on nähe ühte ühelõimelist protsessi.
	Protsessil on enda lõimetabel
	Protsess võib kasutada enda planeerimisalgoritmi.
	Probleemid:
		Ei saa kasutada mitut protsessorit
		IO taga olek viib kogu protsessi ja seega kõik lõimed blocked staatusesse
		Puuduvad katkestused, mis võtavad protsessi sees täitmisjärje.
	Näited:
		POSIXi Pthreads
		Machi C-threads
		Windows NT fiibrid (kiud on osa lõimest)
Tuuma lõimed
	Toetatud tuuma poolt, tuuma jagab nende lõimede vahel aega.
	Haldus kulukam kui kasutajatasemel
	Võimalik jooksutada mitmel CPU-l.
	I/O blokk ei takista teise sama protsessi lõime tööd.
	Sisuliselt igal protsessil võimalik vähemalt üks tuuma lõim.

Saab kasutada mõlemat, nii üks-ühele kui üks mitmele tuuma vs kasutajataseme lõimesid. Tra okei võib ka mitu mitmele, aga see ei tähenda otseselt üks-ühele. Aina keerukamaks läheb.

Lõimedega saab Pthreadsis mugavalt suhelda, aga ei ole soovituslik kui sa ei tea, mida sa teed.
Windowsi lõimed
	Windowsis on rohkem lõime ja protsesse kui Linuxis.
	Üks-ühele mudel.
	Kaks magasini kasutaja ja tuuma jaoks.
	Igal lõimel privaatne ala.