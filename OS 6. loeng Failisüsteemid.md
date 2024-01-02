Umask (User file creation mask)
	Linuxis kasutatakse vaikefaili- või kataloogilubade režiimide määramiseks.
	Eesmärk on kontrollida uute failide või kataloogide loomisel määratud vaikeõigusi, tagades, et neile ei antaks kogemata liiga lubavaid õigusi.
	umask väärtustatakse sisselogimise ajal
	umask õigused = 777 - väärtus
	vaikimisi 022, kus uued failid 644, kataloogid 755
	Vaikimisi ei anta failidele käivitusõigust, see tuleb vajadusel käsitsi lisada.

Sticky bit (chmod +t)
	Luba, mida saab määrata kataloogidele ja mis mõjutab failide kustutamise õigust sellest kataloogist.
	Sellises kataloogis saavad faile kustutada või ümber nimetada ainult faili omanik, kataloogi omanik ja juurkasutaja, olenemata faili individuaalsetest õigustest.
	Selle esmane eesmärk on pakkuda turvalist keskkonda jagatud kataloogidele, näiteks /tmp, kus mitu kasutajat saavad faile luua.
	Kui kataloogil pole teiste jaoks täitmisõigusi, aga on sticky bit, siis kuvatakse T suurena (viimane x puudu)

Executable bit
	Võimaldab faili käivitada.
	Faili käsitletakse programmi või skriptina ning seda saab käivitada.
	Täpsem olemus sõltub faili tüübist:
	Binaarsed käivitatavad failid: võimaldab binaarfaili programmina
	Skriptid: ei ole käivituseks lisaks tõlki vaja, saab otse käivitada.

Juurdepääsu kontrolli loend (Access control list) (ACL)
	Failidele ja kataloogidele üksikasjalikumad õigused, võimaldades õigusi suvalistele kasutajatele ja rühmade loendile. Ületab klassikaliste lubade piirangud.
	Kõik failisüsteemid ei toeta ACL-i. Selle haldamine võib olla keerulisem kui traditsiooniliste õiguste haldamine, eriti, kui tegemist on suure hulga kasutajate ja rühmadega.


Täiendavad atribuudid (chattr)
	Saab määrata või kustutada faili või kataloogi teatud atribuute.
	i - muutumatu, ei saa faili muuta, kustutada ega ümber nimetada. Isegi mitte juurkasutaja.
	a - ainult lisamine
	s - turvaline kustutamine, nullitakse seal olevad plokid välja, et andmeid ei saaks taastada.
	A - atime puudub, takistab viimati kasutatud ajatempli värskendusi
	u - undeletable, isegi pärast kustutamist saab andmeid taastada.


Failisüsteem
	On meetod ja andmestruktuur, mida OS kasutab salvestusmeediumil olevate failide haldamiseks ehk kuidas andmeid ja metaandmeid säilitatakse.
	FAT32 süsteemis 4GB faili max suurus
	Fail on ühikusse salvestatud andmete kogum, mida identifitseerib failinimi. See võib olla dokument, pilt, heliriba, andmestruktuur või mis tahes muu teabekogu. Põhimõtteliselt esindab fail kindlat andmekogumit andmekandjal.
	Kataloog on konteiner, mida kasutatakse failide ja muude kataloogide korraldamiseks. See annab võimaluse seotud failide rühmitamiseks ja moodustab aluse failisüsteemi hierarhilise puu struktuurile.


Faili metaandmed
	Loomise kuupäev
	Muutmise kuupäev
	Suurus 
	Faili tüüp
	Õigused
	Omanik 
	Asukoht

Salvestusmeedium
	Viitab mis tahes füüsilisele seadmele või materjalile, millele saab andmeid elektrooniliselt salvestada. Säilitab teatud aja jooksul kas ajutiselt või püsivalt andmetöötluseks digitaalseid andmeid.

Salvestuskandja tüübid
	Ebapüsiv, lenduv, volatile - andmed kaovad, kui toide välja lülitatakse.
	Püsiv, mittelenduv, non-volatile - andmed säilitatakse isegi väljalülitatuna.

Salvestuskandja näited
	HDD
	SSD
	USB-drive
	Optilised plaadid
	Flopikettad
	Magnetlindid
	RAM
	Mälukaardid ja SD-kaardid 

Salvestuse kategooriad
	Kohalik salvestusmeedium - füüsilised arvutiga ühendatud seadmed
	Võrgustatud salvestuslahendused - ligipääs võrgu kaudu
	Pilvesalvestuslahendused - majutatakse andmekeskustes, võivad levida mitmesse kohta üle maailma ja millele pääseb ligi interneti kaudu. Skaleeritav salvestusmaht ja lisafunktsioonid 

Plokitasemel ja failitaseme juurdepääs 
	Plokitasemel sektorite kaupa, detailsem, failitasemel tegeldakse plokitasemel kasutaja eest.
	Plokitasemel tagab kõrge kontrolli ja jõudluse, aga pole kasutajasõbralik ega ohutu. Võib hooletusest faile rikkuda.
	Failitasemel sobib paremini igapäevaseks tegevuseks, aga ei ole nii paindlik ja puudub otsene juhtimine.


Eriomadused
	Päeviku pidamine (journaling) - peetakse tehtavate muudatuste päevikut, tagades, et voolukatkestuse või krahhi korral toimub taastamine kiiremini ja ilma andmete rikkumiseta.
	ext3, ext4, NTFS, ReiserFS, JFS, XFS
	Hetktõmmised (snapshots) - failisüsteem säilitatakse teatud ajahetkel, võimaldades hõlpsalt süsteemi varundada ja taastada.
	Btrfs, ZFS, LVM