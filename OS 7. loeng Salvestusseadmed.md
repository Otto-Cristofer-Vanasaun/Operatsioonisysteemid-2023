Ketas kui loogiliste plokkide jada (plokkseade)
	Plokkidele seatakse vastavusse sektorid
		Tänapäeval enamasti 4096 baiti
		Näidatakse ühilduvuse huvides OS-le 512-baidist sektorit
	Sektorite paigutamin vea korral (reallocation
	Silindrid, rajad, sektorid (raja sektor on üks hor.-kiht rajast)
	Silinder läbib kõiki vert.-kihte, selle ühe kihi nimetus on track. Sellel on klastrid, milles omakorda sektorid.
	Ühes sektoris ei ole mitut faili (aga üks fail võib olla mitmes sektoris)
	Füüsiline struktuur
		Taldrikud (platters)
			Kõvaketas koosneb ühest või mitemest lamedast ümmargusest kettast, mida nimetatakse taldrikuteks ja mis salvestavad andmeid. Pöörlemiskiirus nt 5400RPM, 7200RPM, 10000RPM
		Pead (heads)
			Lugemis- ja kirjutuspead on väikesed andurid, mis liiguvad plaatide kohal, et lugeda või kirjutada andmeid.
		Rajad (tracks)
			Rada on konsentriline ring taldriku peal. Igal taldrikul on tuhandeid radu.
		Sektorid
			Väikseim ketta adresseeritav üksus (512B-4KiB)
		CHS aadress
			silinder-pea-sektor
			Kaasaegsed draivid on juba ammu ületanud CHS-i adresseerimispiirangud, seega kasutatakse nüüd loogilist ploki adresseerimist (LBA), kus iga sektori jaoks on unikaalne number
		Sektorite klasterdamine
			OS ei halda tavaliselt andmeid sektori tasandil
		SSD-seadmed
			Seek on tasuta, ülekandekiirus arvestatav kuni väga hea
			Piiratud kirjutamiste arv samale sektorile
			Toite kadumisel kaotatakse terve erase plokk mitte sektor
			Wear leveling - meetodid kogu kettapinna ühtlaselt vananemise tagamiseks
			TRIM lisakäsk mittevajalike alade vabastamiseks (et osa kirjutamisel ei oleks vaja vana seisu lugeda)
			Vajalik plokkide joondamine (alignment) erase block mahule
			OS: unustada pöörlemist eeldavad IO planeerijad
		Ketaste ühendamine
			Otse arvuti külge
				SATA, NMVe, USB
			Salvestusvõrgu kaudu
				SAN (Storage Area Network)
				Oma protokollistikuga võrk salvestusseadme ja serverite vahel
				Switched FibreChannel (32-128G)
				IP võrk (+1G/10G/40G/100G Ethernet jms)
				Infiniband (kuni 300G) + RDMA
		Kettapöörduste planeerimine
			OS vastutab kettapöörduste efektiivsuse eest
				Läbilaskekiirus suureks
				Viivitus väikeseks
			Pöördusajal on kaks olulist tegurit
				Raja otsimine - aeg sõltub sellest, kui palju on vaja pead liigutada
				Rajalt sektori otsimine (keskmiselt pool pööret)
			Läbilaske maksimaalne kiirus sõltub kettaseadmest
			OS tahab liigse positsioneerimise välja optimeerida, et läbilase oleks maksimumi lähedane
			Kui meil on ketta järjekorda kogunenud päringud mingile sektorile, mis järjekorras neid täita, et viivitus vähim oleks?
			FCFS (first come first served), keskel asuvaid sektoreid teenindatakse kiiremini
			C-SCAN - nagu SCAN, aga tagasiteel ei teenindata
			C-LOOK
		Algoritmid Linuxis
			NOOP (päringute kokkukleepimine)
			Deadline (prioriteet vastavalt interaktiivsusele, näljutamise vastu tähtaeg)
			CFQ (klassidest vaheldumisi, arvestab IOga)
			MQ-Deadlin, Kyber, BFQ - mitme järjekorraga variandid
		Ketaste ette valmistamine
			Madala taseme - sektormärkide radadele kandmine
			Tänapäeval ei paista reeglina OS-le enam kätte
			Partitsioneerimine - ketta osadeka jagamine
			Loogiline formaatimine ehk failisüsteemi tekitamine
			Bootloaderi paigaldamine
			Vigaste kettaplokkide leidmine ja meelde jätmine
		Madala taseme formaatimine
			Cylinder skew - erinevate radade sektorid on üksteise suhtes nihkes
			Aitab vähendada pöördumisviivitust järjestikuste sektorite lugemisel mitmelt rajalt
			Vahelejätt (interleaving) - sektorid paigutatakse üle ühe
			Aitab vähendada olukorda, kus eelmise sektori andmete ülekandmise ajal liigub lugemispea üle järmise sektori
			Aeglasema ülekandekanali puhul kasutatakse ka üle kahe vahelejättu
		Saalimisala haldamine
			See on protsesside või lehekülgede salvestusruum virtuaalmälule
			Eraldi kettal/partitsioonil (Linux swap)
			Eelallokeeritud failis Windows pagefaile.sys
			Saalimisala protsessi kogu virtuaalmälu kohta (BSD Unix)
			Saalimisala reaalselt välja saalitud mälulehekülgede kohta (Solaris, Linux...)
			RAM-is peab saalimisala kohta kaart olema.
		RAID massivid
			Redundant Array of Inexpensive Disks
			Paralleelsuse kaudu kiiruse ja töökindluse suurendamine
			Peegeldamine (mirroring)
			Paarsusinfo laiali jagamine (interleaved parity)
				Bitikaupa
				Plokikaupa
			Parandusaeg peab mõistlik olema
			Kuumvaru (hot spare), ketaste kolimine
			Tarkvaraline vs riistvaraline RAID (NVRAM vahemälu)
			RAID 0 - mitmest kettast ühe suure tegemine
			Virtuaalne ketas koosneb vöötidest (stripe)
			Vöödid on jagatud n ketta vahel
			Kõrvuti olevate vöötide lugemine võib toimuda paralleelselt
			RAID 1 - peegeldamine (sama info mitme seadme peal)
			RAID 2 - Mälu stiilis veaparanduskoodid
				Vöödid on väikesed (biti, baidi suurused)
				salvestatakse Hammingi kood
				Ühe ketta veast suudab taastuda
				Vajab log lisakettaid
				Harva kasutusel
			RAID 3 - bitihaaval paarsuskontroll
			RAID 4 - plokihaaval paarsuskontroll
				suuremad vöödid kui RAID 3-l
				paarsusketas võib osutuda pudelikaelaks
			RAID 5 - plokihaaval hajutatud paarsuskontroll
				paarsussektorid hajutatud ketaste vahel
			RAID 6 - kahemõõtmeline paarsuskontroll
			RAID 0+1 - peegeldatud stripepaarid
				Kannatab ühe ketta viga igast peeglipaarist
			RAID riistvaras ja tarkvaras
				Enamik tasemeid saab mõlemas realiseerida
				Riistvaras CPU koormust vähemaks
				Tarkvaras CPU võib olla kiirem kui RAID kontrolleri protsessor, OS-il RAID on kergemini hallatav
				BIOS RAID - võimalus bootida muudelt RAID-idelt kui 1, hädalahendus, kui OS-i RAIDi ei saa kasutada
				RAID failisüsteemi tasemel
					Liiasust ei pea realiseerima plokkseadme tasemel, vaid võib teha ka failisüsteemi siseselt
				LVM - logical volume management
					abstrahheerib salvetussüsteemist välja füüsilised kettad
					füüsiline ketas jagatakse partitsioonideks
					peidetakse füüsilised kettad ära, OS-ile näidatakse ainult loogilisi köiteid
					Neid köiteid võivad tegelike ketaste osade vahel suvaliselt jaguneda
					Tegelikud kettad jagame väikesteks tükkideks, mida saab köideteks grupeerida
				NAND välkmälu
					SLC - 1 bitt lahtri kohta. Kiireim ja vastupidavaim
					kirjutamine hõlmab selle elementide laetuse oleku muutmise, mis võib aja jooksul kuluda. 
