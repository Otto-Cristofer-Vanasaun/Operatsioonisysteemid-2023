Objektifailide sidumine
	Objektfailide ja teekide ühendamise protsess käivitatava- või teegifaili loomiseks.
	See on samm pärast kompileerimist, mis muudab lähtekoodi objektifailideks. Linkimine on staatiline või dünaamiline.
	Staatiline: objektfailid ja teegid ühendatakse üheks käivitatavaks failiks. Iseseisev, kuid suur tulemus.
	Dünaamiline: käivitatav fail sisaldab vaid viiteid välistele teekidele. Need lahendatakse käitusajal, vähendades failisuurust, kuid lisades sõltuvusi.
	Ohud: protsessid võivad vajada eri versioone programmidest, Linuxi versioonihaldur lahendab selle.

Aadresside sidumine
	Keelekonstruktsioonide sidumine mäluaadressiga võib toimuda erinevatel etappidel:
		Staatilise kompileerimise ajal - mälupaigutus on ette teada, genereeritakse kood absoluutaadressiga, paigutuse muutumisel on vaja ringi kompileerida
		Laadimise ajal, dünaamiliselt lingitud - genereeritakse mälus ümberpaigutatav kood, reaalsed mäluaadressid asendatakse programmi laadimisel 
		Täitmise ajal, dünaamiliselt laetud - aadresside sidumine lükatakse edasi konkreetse aadressi poole pöörumiseni. Programmi saab täitmise ajal mälus ringi liigutada. Vajab riistvaralist tuge. Täitmise ajal ei teata, kui palju mälu programm tegelikult vajab.

Loogilised ja füüsilised aadressid
	Nende eraldamine on üks mäluhalduse olulisemaid kontseptsioone
		Loogiline aadress - programmide poolt kasutatav aadressiruum, nimetatakse ka virtuaalseks aadressi ruumiks
		Füüsiline aadress - aadress, mida mäluseade tegelikult näeb ja kasutab. Kompileerimise ja laadimise ajal seotavate aadresside puhul on loogiline ja füüsiline aadress samad, täitmise ajal seotavatel erinevad
	MMU (Memory Management Unit) - riistvaraline seade loogiliste aadresside füüsiliseks teisendamiseks
	Kasutajaprogramm tegeleb oma loogiliste aadressidega (0...max) ega näe otseselt füüsilisi aadresse.

Füüsiline aadressiruum
	Viitab tegelikult süsteemi installitud RAM-ile. Kui protsessor pääseb juurde andmetele või juhistele, tõlgitakse see lõpuks asukohta füüsilises mälus. Füüsilist aadressiruumi haldab OS koos riistvarafunktsioonidega, nagu mäluhaldusüksus (MMU).

Loogiline aadressiruum
	Tuntud ka kui virtuaalne mäluruum, see on abstraktsioonikoht programmi ja füüsilise mälu vahel. Iga süsteemis töötav protsess näeb oma külgnevat aadressiplokki, mis tavaliselt algab nullist. OS ja MMU on selle loogilise aadressiruumi toovad vastavusse füüsiliste aadressidega.

Dünaamiline linkimine
	Linkimine lükatakse edasi täitmise ajaks
	Tegeliku alamprogrammi asemel on proksi (stub), mis esimesel temal poole pöördumisel laadib päris alamprogrammi ja asendab ennast selle alamprogrammiga (enamasti viida vahetusega).
	OS tuge on vaja juhul, kui tahame neid alamprogramme jagada mitme protsessi vahel ja kasutame seejuures mälukaitset
	Eriti kasulik (süsteemsete) teekide kasutamisel - kettaruumi ja mälu kokkuhoid, mugav teekide uuendamine.
	Linkimisega tegeleb OS laadija.
	Kasulik näiteks siis, kui harva esinevate erijuhtude jaoks on kokku palju koodi, mida ei ole alati just vaja laadida.
	Mälukasutus on efektiivsem.
	Käitusaeg: teegid laaditakse töötavasse programmi nõudmisel.
	Programmi hallatav: programm ise haldab laadimise, kasutades süsteemikutseid, nagu dlopen() või LoadLibrary()
	Aadressi sidumine: programm otsib selgelt sümboleid, tavaliselt nime järgi, ja aadressid seotakse käitusajal.
	Paindlikkus: suurem dünaamiline linkimine, kuna mooduleid saab lennult laadida ja maha laadida.
	Kasutusjuhtumid: kasulik pistikprogrammides (plugin(?)), laiendusted ja olukordades, mis nõuavad suurt modulaarsust.

Ülekate (overlay)
	Rakendusprogramm hoiab mälus ainult osa programmist ja andmetest, mida hetkel on vaja
	Kasutatakse, kui programm kokku on suurem kui talle antud mälu
	OS tuge pole vaja, realiseeritav kasutaja tasemel
	Näide: DOS ja suured programmid
		mälupiirangud, täpsemalt 640KB tavamälu limiit
		võimaldab programmidel olla olemasolevast mälust suuremad, jagades need väiksemateks osadeks, mida nimetatakse ülekateteks
		vajalikud ülekatted laaditakse käitamise ajal mällu, vahetades vastavalt vajadusele sisse ja välja.

Saalimine (swapping)
	Protsessi võib mälust ajutiselt välja salvestusruumi kirjutada ning hiljem tagasi mällu laadida.
	Salvestusruum - kiire plokkseade, mis mahutab kõigi kasutajaprogrammide mälukujutised, peab olema otsejuurdepääsuga suvalise mälukujutise juurde
	Roll out/roll in - saalimise variant prioriteedil põhinevate planeerimisalgode juurde: madalama prioriteediga protsess saalitakse välja kõrgema töö ajaks.
	Enamiku saalimise ajast võtab andmete kopeerimine välisseadmele, aeg on lineaarselt sõltuv mäluhulgast.
	Muudetud kujul on saalimine kasutusel ka tänapäeva süsteemides, näiteks Unix, Linux, Windows

Pidevate mälualade hõivamine
	Põhimälu on enamasti jagatud kahte ossa
		Residentne OS (tihti madalamatel mäluaadressidel katkestusvektori asukoha tõttu)
		Kasutajaprotsessid
	Kasutajaprotsesside mälu on omakorda jagatud tükkideks
	Igale täidetavale protsessile eraldatakse üks sobiva suurusega terviklik mälutükk
	Auk - vaba mälutükk (uued protsessid saavad mälu nendest)
	Iga protsessiga on seotud teisaldus- ja piiriregister
		Kasutatakse loogilisete aadresside teisendamisel
		Kaitseb protsesse ja OS-i vigaste mälupöördumiste eest
	Kasutajaprotsessidele mõeldud mälu tükkideks jagamine võib toimuda staatiliselt või dünaamiliselt
	Staatilise tükelduse korral on tükkide arv ja suurus eelnevalt fikseeritud
		kõik tükid on võrdse suurusega
		erineva suurusega tükid
	Erijuht - monoprogrammeerimine, kus korraga täidetav ainult üks protsess, millele antakse kogu OS-ist üle jääv mälu

Fikseeritud tükeldusega mälujaotus
	Võrdse suurusega tükid
		Protsess, mille suurus ei ületa tüki suurust, laetakse suvalisse vabasse tükki
		Kui kõik tükid on hõivatud, võib OS mõne protsessi välja saalida
		Kui programm ei mahu tükki ära, peab programmeerija kasutama ülekatmist
	Lihtne realiseerida, kuid mälukasutus on ebaefektiivne
		Sisemine fragmenteerumine - ükskõik kui väike ka protsess ei oleks, võtab ta enda alla terve tüki
	Erineva suurusega tükid
		Protsessile antakse vähima suurusega tükk, millesse ta ära mahub
	Igal tükil (või sama suurusega tükkidel) üks eraldi protsesside järjekord
		Vähendab sisemist fragmenteerumist
		Ebaefektiivne mitmetegumilisus
	Üks globaalne sisend järjekord
		Valida esimene protsess, mis auku mahub
		Valida suurim protsess, mis auku ära mahub
		Teisel juhul näljutamise oht

Dünaamilise tükeldusega mälujaotus
	Tükkide arv ja suurus ei ole eelnevalt fikseeritud, vaid muutub vastavalt täidetavate protsesside arvule ja suurusele
	Protsessile antakse täpselt nii suur tükk, kui ta vajab
	Protsessi lõpetamisel või välja saalimisel vabanev tükk ühendatakse võimalusel ümbritsevate aukudega suuremaks auguks
	Kalduvus tekitada kasutuses olevate tükkide vahele väikseid auke
	Väline fragmenteerumine - vajalik mälu leidub, aga ta ei ole sidus
	Probleem: kuidas rahuldada päringut mäluplokile pikkusega n etteantud aukude nimekirjast?
		Esimene sobiv (first fit)- kasutatakse esimest piisava suurusega auku. Esimest võib lugeda algusest või eelmisest leitud august alates.
		Parim sobiv (best fit) - kasutatakse vähimat piisava suurusega auku. Ajakulukam.

Fragmenteerumine ja tihendamine
	Saab vältida mitmete väikeste mäluaukude teket.
	Compaction. Tõstame hõivatud mälualasid ümber, näiteks kõik ühte otsa kokku
	Võimalik ainult dünaamilise ümberpaigutamise korral
	Pooleli olev I/O segab (kopeerime OS puhvritesse või jätame protsessi paigale)
	Suhteliselt kulukas

Mäluhaldus bititabelitega
	Süsteem peab pidama arvet hõivatud ja vabade mälupiirkondade üle
	Lihtsam meetod on kasutada bititabelit
	Kõrvuti olevate aukude ühendamine on automaatne
	Piisava suurusega vaba piirkonna leidmine on aeglane

Mäluhaldus listidega
	Iga tüki jaoks peame meeles tema staatuse, alguse ja pikkuse
	Vastavat infot hoiame dünaamilises listis (P - process, H - hole)
	Kõrvuti olevate aukude ühendamine on lihtne
	Piisava suurusega vaba piirkonna leidmine on kiirem kui bititabeli korral, kuid siiski lineaarse keerukusega.
	Variatsioonid
		Haldame eraldi listi vabade ja hõivatud tükkide kohta
			Piisava suurusega vaba tüki leidmiseks pole vaja enam hõivatud tükke inspekteerida
			Pole enam vajadust stabiilsusbiti (P/H) järele
			Vabade tükkide listi jaoks pole eraldi mälu vaja, kuna neid tükke saab ise selleks ära kasutada
			Kõrvuti olevate aukude ühendamine on suhteliselt kulukas
		Haldame sagedasti esinevate tükisuuruste jaoks eraldi vabade tükkide listi
			Piisava suurusega tüki leidmine on kiire

Buddy süsteem
	Kui kogu olemasolevat mälu käsitletakse kui üht mälutükki suurusega 2 U
	Kui küsitava mälu suurus on 2U-1 <= n <= 2 U, siis hõivatakse kogu tükk
	Vastasel korral jaotatakse tükk kaheks võrdseks osaks ja kogu protsessi korratakse kuni sobiva tüki tekkimiseni
	Tüki vabastamisel kontrollitakse kas "kaastükk" on vaba

Lehekülgede saalimine (paging)
	Protsessi füüsiline aadressiruum ei pea tingimata olema pidev - protsessi eri osad võivad asuda füüsilises mälus suvaliste kohtade peal laiali
	Jagame füüsilise mälu fikseeritud suurusega lehekülgedeks (kaadriteks - frame), suurus kahe aste (2048, 4096, 8192 jne)
	Jagame loogilise mälu samasugusteks lehekülgedeks (page) 
	Peame arvet vabade kaadrite üle
	Suurusega n protsessi jaoks otsime lihtsalt n vaba kaadrit
	Iga protsessi kohta teeme leheküljetabeli loogiliste lehekülgede ja füüsiliste kaadrite vastavusse seadmiseks
	NB! Lehekülgede kaupa hõivamisel tekib paratamatult sisemine fragmenteerumine

Aadresside tõlkimine
	Mäluaadressi bitid jagatakse kahte gruppi
		Lehekülje number(p) - kasutatakse indeksina leheküljetabelisse lehekülje füüsilises aadressi leidmiseks
		Nihe lehekülje sees (d) - liidetakse lehekülje füüsilisele aadressile täieliku aadressi saamiseks
	Kontekstivahetuse ajal programmeerime MMU vastavalt protsessi leheküljetabelile
	Ühesõnaga liidetakse mäluaadress ja lehekülje indeks, lõplik aadress koosneb neist kahest argumendist.

Leheküljetabelite realiseerimine
	Tabelid hoitakse mälus
	Algust näitab vastav register (PTBR)
	Pikkust näitab kah vahel register (PTLR)
	Iga soovitav mälupöördus nõuaks kaht tegelikku pöördust
	Seda probleemi lahendab viimati- (sagedamini?) kasutatud kirjete puhverdamine protsessori või MMU sees
	TLB (Translation Lookaside Buffer) assotsiatiivmälu abil realiseeritud leheküljetabeli kirjete puhver
	TLB miss - ei leita TLB-st, tuleb mälust lugeda (vastand TLB hit-le)
	ASID (Address Space ID), virtuka märgistatud TLB
	TL;DR loogilisest füüsilise lehekülje aadressi saamine on kiirem, ei pea leheküljetabelist seda otsima iga kord, kui see on TLB-s salvestatud.

Efektiivne mälupöördusaeg
	Reaalne mälupöördus = 1 ajaühik
	Assotsiatiivmälust otsimine = q ajaühikut
	Assotsiatiivmälu edukate otsimiste osakaal (hit ratio) - mitmel protsendil juhtudest TLB hit

Mälukaitse
	Igal leheküljel lipp valid
		valid - lk on protsessi mälupiirkonnas
		invalid - ei ole
	Näiteks märgistatakse mälupiirkonna lõppu sellega.