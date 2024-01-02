Efektiivne mälupöördusaeg
	Efektiivne mälu juurdepääsu aeg (EAT) kvantifitseerib keskmist aega, mis on vajalik mälukohale juurdepääsuks, kaasa arvatud potentsiaalse vahemälu möödalugemise poolt sisse toodud latentsus. See on mõõdik, mida kasutatakse arvutisüsteemides vahemälu toimivuse hindamiseks.
	EAT arvutus arvestab vahemälus tabamisi (hit) ja mödalugemisi (miss). Vahemälus tabamine toimub siis, kui protsessori poolt nõutav andmed on vahemälus olemas. Miss on põhimälust toomine.
	Epsilon tähistab assotsiatiivmälu otsinguaega.
	Alpha tähistab vahemälu tabamise suhet, mis on mälulue juurdepääsu osakaal.
	1 on ajaühik andmetele juurdepääsuks eeldades tabamist.
	2 on ajaühik juurdepääsuks põhimälust ja aega uuendamiseks.
	EAT arvutatakse korrutades tabamise tõenäosusega + aeg, mis kulub möödalugemiseks. Ananb keskmise aja ühe mälujuurdepääsu kohta.

Mälukaitse 
	Saab ja peaks seostama iga lehega.
	Iga lehe jaoks valid lipp.
	valid - on protsessi aadressiruumis
	invalid - ei ole.
	Näiteks saab sedda kasutada mälupiirkonna lõpu tähistamiseks.
	Kaasaaegsetes OS-ides on mälukaitse hädavajalik stabiilsuse ja turvalisuse säilitamiseks. Mälu seostamine iga lehega võimaldab süsteemi kontrollida mitu juurdepääsu granulaarsel tasemel. Valid/invalid lipud on iga lehekülje tabeli kirjest virtuaalmälus.
	Valid lipp näitab, et virtuaalaadress on kaardistatud füüsilisele aadressile ja leht on laetud füüsilisse mällu, et protsess saaks seda kasutada.
	Invalid võib olla siis, kui leht ei ole veel eraldatud, on vahetatud kettale või kasutatakse protsessi lubatud aadressiruumi piiride tähistamiseks.
	Kui protsess üritab lehele juurde pääseda, kontrollib MMU vastava lehe lehekülje tabeli kirjet. Kui valid lipp ei ole määratud, tõstab MMU rikke, mida OS käitleb, näiteks laadides lehe või protsessi lõpetades.
	See süsteem on virtuaalmälu alus, mis võimaldab protsessidel omada isoleeritud aadressiruume, suurendades turvalisust ja stabiilsust.

Hierarhilised leheküljetabelid
	Ühe suure leheküljetabeli vältimiseks kasutatakse mitmerealist (hierarhilist) leheküljetabelit.
	Kaheastmeline leheküljetabel jaotab aadressi leheküljesisese aadressi osaks ja lehekülje numbri osaks, mis omakorda jaguneb kaheks bitigrupiks (iga taseme jaoks üks grupp, mis määrab indeksi vastavas tabelis).
	Näiteks 32-bitilise aadressi puhul, kui lehekülje suurus on 4K (12 bitti), jagatakse ülejäänud 20 bitti kaheks 10-bitiseks osaks lehekülje numbrite jaoks (välimise leheküljetabeli indeks ja sisemise leheküljetabeli indeks).
	Füüsilised leheküljed võivad siiski olla läbisegi (sõltumata kummagi tabeli järjestusest).
	Hierarhiat võib laiendada kolme- ja neljatasemelistele leheküljetablitele ja kaugemalegi, mahutamaks suuremaid aadressiruume.
	Nende kasutamine on kompromiss kiire mälule juurdepääsu vajaduse ja füüsilise mälu suuruse piirangute vahel, võimaldades mälu efektiivset kasutamist säilitades samal ajal kiired aadressi tõlkimise võimed.
	Hierarhilised leheküljetabelid on meetod virtuaalmälu füüsilisele mälule kaardistamiseks ilma, et oleks vaja üht suurt järjestikust mäluhulka üheks monoliitseks leheküljetabeliks. Leheküljetabeli jaotamine mitmeks tasemeks tähendab, et mällu tuleb laadida ainult tabeli vajalikud osad, mis muudab protsessi efektiivsemaks.
		Kaheastmeslise tabeli korral jaotatakse virtuaalne aadressiruum lehekülgedeks. Iga lehekülje number jaguneb osaks, mis valib kirje ülaltasemel (välimises) tabelis, ja osaks, mis valib kirje alamtasemel (sisemises) tabelis.
		Selliine jagunemine vähendab tegelikult vajaliku leheküljetabeli suurust mälus ühel ajahetkel, kuna peab olema kohal ainult hierarhia osa, mis on vajalik antud virtuaalaadressi füüsilisele aadressile tõlkimiseks.
		32-bitistes süsteemides kasutatakse kahte 10-bitist osa, arvestades lehekülje 4K suurust, välimise ja sisemise tabeli indekseerimiseks, viimase 12 bitti aadressist kasutatakse indekseerimiseks lehekülje enda sees.
		Suuremate virtuaalaadressiruumide, nagu 64-bitistes arhitektuurides, korral võib vaja minna täiendavaid leheküljetablie tasemeid, et käsitleda suuremat arvu võimalikke lehekülgi. See viib kolme- või neljatasemeliste tabelie struktuurideni, kus virtuaalaadressi täiendavad bittide gruppe kasutatakse indekseerimiseks iga täiendava tabeli taseme jaoks.

Paisksalvestusega leheküljetabelid
	64-bitises süsteemis võib mitmeastmeliste tabelite kasutamine muutuda ebaefektiivseks tohutu aadressiruumi tõttu.
	Virtuaalse lehekülje number salvestatakse tabelisse paiskfunktsiooni kasutades.
	Leheküljetabel on paisktabel välisahelatega (kokkupõrke lahendamiseks), võimaldades mitmel leheküljel hashida samasse sissekandesse.
	Otsingud on kiired, kuna need hõlmavad lihtsat paiskfunktsiooni ja potentsiaalselt lühikest ahela läbimist.
	Kontesktivahetus võib olla väga aeglane, kuna paiskmehhanism nõuab paisatud sissekannete uuesti valideerimist või tühjendamist uue konteksti jaoks.

Paisksalvestusega leheküljetabelid (Hashed Page Tables)
	Paisksalvestusega tabelid on loodud spetsiaalseks 64-bitiste süsteemide suurte virtuaalaadressiruumide väljakutsetega toimetulekuks. Need on eriti kasulikud, kui korraga on kasutusel ainult väike osa virtuaalaadressiruumist.
		Paiskfunktsioon võtab virtuaalse lehekülje numbri ja arvutab asukoha paisktabelis. Kui kaks virtuaalset lehekülje numbrit paiskuvad samale asukohale (kokkupõrge), sisi kasutatakse väliste ahelate abil kirjete linkimist sama paisktabeli indeksi juures.
		Väliseid ahelaid otsitakse lineaarselt, et leida õige tabeli kirje, mis võib põhjustada veidi pikema otsinguaja, kui ahelad muutuvad pikaks.
		Siiski on võimalik kokkupõrgete tõenäosust ja ahelate pikkust kontrollida sobiva paiskfunktsiooni ja tabeli suuruse valimisega.
		Kontekstivahetuse puhul peab OS tagama, et uuel kontekstil oleks puhal paisktabel või et uue protsessi jaoks olulised kirjed oleksid kehtivad. See võib kaasa tuua märkimisväärse ülekoormuse, eriti, kui paisktabel on suur.
Pööratud leheküljetabel (inverted page table)
	Idee: pööratud leheküljetabel sisaldab kirjet iga füüsilise mälu lehekülje kohta, mitte iga virtuaalse aadressi jaoks
	On ainult üks tabel kõikide protsesside jaoks, mis välistab vajaduse igal protsessil oma tabeli järele, mida kontekstivahetuse ajal peaks vahetama.
	Pööratud leheküljetabeli iga kirje koosneb protsessi identifikaatorist (PID) ja vastavast virtuaalsest lehekülje numbrist protsessis.
	Mälukasutus on väiksem võrreldes traditsiooniliste mitmetasemeliste leheküljetabelitega, sest kirjeid on vähem.
	Lehekülje kirje otsimisaeg võib olla pikem, kuna tabelis tuleb otsida vastavust PID-le ja virtuaalsele lehekülje numbrile.
	Otsimisaja kiirendamiseks võib kasutada paisktabelit, et indekseerida pööratud leheküljetabeli kirjeid, samuti kasutatakse Translantion Lookaside Bufferit (TLB)
	Pööratud leheküljetabelid on eriti kasulikud süsteemides, kus on suur füüsiline mälu ja arvukalt samaaegseid protsesse, kus traditsioonilised tabelid tarbikisid liigselt mälu.
	Struktuur on kaardistus füüsiliselt lehekülje numbritelt virtuaalse aadressiruumi identifikaatorile (PID-dele ja virtuaalsetele lehekülje numbritele), mis on vastupidine tavalistele leheküljetabelitele.
	Kuna iga füüsiline leht omab ainult üht kirjet, mahub tabel täielikult füüsilisse mällu, vähendades vajadust kettalt I/O järele tabeli andmete jaoks.
	TLB on sellises seadistuses kriitilise tähendusega, kuna see hoiaks vahemälus hiljuti kasutatud tabeli kirjeid, vähendades oluliselt pööratud leheküljetabeli otsingute arvu.
	Paisktabel toimib esmatasandi indeksina, mis vähendab skännitatavate kirjete arvu pööratud leheküljetabelis antud virtuaalse aadressi jaoks.
	Pööratud tabel, vähendades mälukasutust, võib tutvustada lisakomplekssust lehekülje otsinguprotsessi. Selle leevendamiseks võidakse rakendada keerukaid paiskfunktsioone ja võimalik, et täiendavaid indekseerimise tasemeid.

Jagatud mäluleheküljed (Shared Memory Pages)
	Koodi sisaldavad lehekülgi on otstarbekas jagada.
	See on võimalik, kui kood on kasutatav (reentrant) - ei muuda iseennast.
	Jagatud lehekülg on nähtav mitme protsessi aadressiruumis.
	Kõvakodeeritud (hardcoded) aadressiga kood peab asuma igas protsessis samal virtuaalaadressil.
	Positsioonist sõltumatu kood (PIC - Position Independent Code) võib asuda igas protsessis erineval virtuaalaadressil (gcc -fPIC).
	Tänapäeval on enamik teekidest postitsioonist sõltumatud.
	Igal protsessil on oma andmed ja tavaliselt ka teatud osa jagamata koodist.
	Pööratud tabelite puhul on jagamine keerulisem seoses nende struktuuriga. 
	Süsteemides, kus mitu protsessi käivitavad sama programmi või kasutavad ühiseid teeke, on mõistlik jagada neid lehekülgi mälu kokkuhoiu eesmärgil.
	Taaskasutatav kood ehk puhas koos ei oma kõrvalmõjusid ega muuda oma juhiseid, mis võimaldab seda turvaliselt jagada (teegid nt libz, libm).
	Kõvakodeeritud või isemuutuv kood võib jagatud mälu keskkonnas põhjustada komplikatsioone ning seda püütakse vältida tänapäeva süsteemides.
	Positsioonist sõltumatu kood on loodud töötama mis tahes mäluaadressil, mis teeb sellest väga sobiva lahenduse jagatud teekide jaoks, mis peavad olema kaardistatud erinevate protsessie aadressiruumidesse.
	Jagatud teekide kasutamine on levinud, et võimaldada ühise koodi jagamise mitme rakenduse vahel, vähendades kogu mälujalajälge.
	Privaatsed andmed ja kordumatud koodiosad ei ole jagatud ning jäävad iga protsessi ainuomaseks, tagades andmete isoleerituse ja turvalisuse.
	Pööratud tabelid kaardistavad füüsilist mälu virtuaalruumi, muutes jagatud virtuaallehekülgede halduse vähem lihtsaks võrreldes traditsiooniliste mitmetasemeliste leheküljetabelitega, kus iga protsessi virtuaalselt-füüsilised kaardistuded on eraldi.

Segmenteerimine
	On mäluhaldusskeem, mis jagab mälu erinevateks segmentideks, selle asemel, et kasutada üht suurt järjepidevat loogilist aadressiruumi.
	See sobitud paremini paljude kasutajate kontseptuaalse maailmavaatega.
	Programm koosneb segmentide komplektist; segment on loogiline üksus nagu:
		Põhiprogramm
		Protseduur, funktsioon, meetod
		Objekt või moodul
		Kohalikud muutujad, globaalsed muutujad
		Magasin (stack ehk lokaalsed muutujad ja funktsiooni kutsungid)
		Võimaldab programmide jaotamist erineva suurusega üksusteks, mida saab paindlikumalt hallata kui võrdse suurusega lehekülgi.
		Iga segment algab baasaadressilt ja ulatub määratletud piirinim pakkudes võimalust toetada moodulpõhist programmeerimist, eraldades koodi ja andmeid.
		Sageli kasutatakse segmente koos leheküljestamisega, kus iga segment jaotatakse eraldi lehtedeks, et hõlbustada vahetamist ja minimeerida fragmenteerumist.
		Loogilisi üksusi nagu protseduurid või objektid saab eraldi kaitsta ja hallata, pakkudes lisakihti turvalisusele ja potentsiaalselt parandades vigade isoleerimist.
		Magasin ehk stack on mälu segment, kus tavalisel hoitakse funktsioonide parameetreid, tagastusaadresse ja lokaalseid muutujaid.

Segmenteerimisega arhitektuur
	Loogiline aadress koosneb paarist: segmendi number ja nihe
	Segmendi tabel seob iga segmendi numbri mäluplokiga:
		Baas - segmendi alguse füüsiline aadress
		Limiit - segmendi pikkus
	Segmendi tabeli algust näitab konkreetne register (STBR - Segment Table Base Register)
	Segmendi tabeli pikkust hoiab tavaliselt register (STLR - segment table length register), mis tegelikult esindab maksimaalset kasutatavat segmendi numbrit.
	Mälu eraldatakse tervete segmentidena (kasutades strateegiaid nagu first-fit või best-fit), mis võib põhjustada välist fragmenteerumist.
	Segmente saab jagada protsesside vahel, hõlbustades protsessidevahelist suhtlust või jagatud teekide kasutamist.
	Segmentatsioon võimaldab peeneteralise juurdepääsu kontrolli, iga segment omab oma juurdepääsuõiguste komplekti (lugemine, kirjutamine, täitmine), suurendades turavlisust ja takistades lubamatu juurdepääsu.
	Loogilise aadressi genereerimisel kasutatakse segmendi numbrit indeksina segmendi tabelis ja baasaadressi leidmiseks, millele siis lisatakse nihe.
	Kui nihe on suurem kui segmendi limiit, genereeritakse segmenteerimisviga, hoidmaks ära ülevoolu teistesse segmentidesse.
	Segmendi muutuva suuruse tõttu on vaba mälu haldamine keerukam võrreldes leheküljestamisega, mis kasutab fikseeritud suurusega blokke. Segmentide jagamine võib olla tõhusam kui lehekülgede jagamine, sest kui jagada on vaja vaid mõned baidid, ei pea dubleerima tervet lehekülge, selle asemel jagatakse ainult asjakohane segment.

Segmenteerimine ja mälukaitse
	Mälukaitse sobitud segmenteerumisega loomulikult, kuna igale segmendile saab seosetada järjepideva juurdepääsuõiguse komplekti. Need õigused on seotud segmendi kirjeldajada segmenditabelis:
		kehtiv/valid näitab, kas segment on kasutuses või mitte
		lugemise kirjutamise ja kävitiamise loa bitid saab seada mis tahes kombinatsioonis, et kontrollida juurdepääsu segmendile
			Lugemise bitt: segmendist lugemine lubatud
			Kirjutamise bitt: segmendile kirjutamine lubatud
			Käivitamise bitt: segmendis koodi käivitamine lubatud
	Lisaks tagavad need kaitsebitid, et segmendi kaitsetaseme poolt mitte lubatud toimingud põhjustavad vea, takistades volitamata juurdepääsu ja pakkudes mehhanismi protsesside isoleerimiseks.
	Mõned süsteemid võivad sisaldada ka muid bitte täiendava granulaarse juhtimise jaoks, nagu 'copy-on-write' bitt, mida kasutatakse optimeerimiseks mälukorralduses või jagatud segmentides.
	Segmenteerimine aitab mitte ainult korraldada mälu loogilisteks plokkideks, vaid pakub ka põhialust turvapoliitikate jõustamiseks mälukorralduse tasemel.
	Segmenditabel hoiba kõikide segmentide kirjeldajaid ja seda viidatakse MMU poolt aadressi teisendamise protsessi ajal. MMU kontrollib segmendi kirjeldaja kaitsebitte enne kui lubab mälupääsu jätkata.
	Kui segmenteerimist kombineerida leheküljendusega, võib see pakkuda kahekordset kaitsemehhanismi, kus nii segmendi kui ka leheküljel on oma kaitsebitid, mis veelgi tõhustavad süsteemi turvamudelit.

Aadresside teisendamine segmenteerimisel
	Loogiline aadressi jaotus
		Loogilises aadressis segmenditud mälu mudelis on kaks osa: segmendi number ja nihe (tuntud ka kui võrdlus või kaugus). Segmendi number identifitseerib, millise segmendi aadressile viidatakse, samas kui nihe tähistab asukohta selles fragmendis.
	Segmenditabeli otsing:
		Segmendi numbrit kasutatakse indeksina segmenditabeli kirje otsimiseks. Segmenditabel on salvestatud mälus ja sellel on baasregister (STBR), mis osutab selle algusele. Iga kirje segmenditabelis sisaldab segmendi baasaadressi füüsilises mälus ja segmendi limiiti.
	Baasaadress:
		Segmenditabelis kirjes olev baasaadress annab segmendi algse füüsilise aadressi mälus.
	Limiidi kontrollimine
		Segmenditabeli kirje limiidi väärtust kasutatakse selle tagamiseks, et nihe on segmendi piires. Kui nihe ületab limiiti, tekib segmenteerimisviga (segmentation fault), kuna see tähendab, et aadress on väljaspool segmendi ulatust.
	Füüsilise Aadressi arvutamine:
		Kui nihe on segmendi limiidi sees, arvutatakse füüsiline aadress lisades nihke segmendi baasfüüsilisele aadressile.

Segmenteerimine koos lehekülgedega (segmentation with paging)
	Multics süsteem lahendas välise fragmenteerumise probleemi, jagades segmendi tabelid lehekülgedeks - iga segmendi tabeli kirje viitas vastava segmendi lehekülje tabelile.
	Selline kombineeritud lähenemisviis on endiselt kasutusel tänapäeva süsteemides.
	Intel 386 arhitektuur (ja järgnev x86 liin) kasutab tõepoolest nii segmenteerimist kui ka lehekülgi. Esialgu pääsetakse ligi segmendi tabelile, et saada lineaarne aadress, millele seejärel rakendatakse kaheastmelist lehekülje tabelit.
	Segmenteerimise ja lehekülgede kombineerimisega on võimalik ära kasutada mõlema eelised, ehkki see toob kaasa täiendava mälukasutuse ja keerukuse nii OS-is kui ka protsessoris.
	OS peab haldama nii segmendi kui ka lehekülje tabeleid, mis suurendab süsteemikõnede arvu ja kontekstivahetuse aega, kui see võimaldab peeneteralisemat mälu kaitset ja haldust.
	Segmenteerimine pakub seotud informatsiooni, nagu kood, andmed ja stack, loogilist grupeerimist, mis võib parandada süsteemi loetavust ja hooldatavust.
	Lehekülgede kasutamine võimaldab aga füüsilise mälu tõhusat kasutust ning teeb virtuaalmälu rakendused efektiivsemaks, võimaldades mittejätkuvat mälu eraldamist.
	Praegusteks x86-64 süsteemides on segmenteerimine endiselt olemas, kuid vähem esiletungiv; domineerivaks on muutunud lame mälumudel ja segmenteerimist kasutatakse peamiselt konkreetsete ülesannete jaoks nagu lõimelokaalne salvestusruum.
	Lisaks kasutavad kaasaegsed süsteemis keerulisi riistvaralisi mäluhaldusüksuseid MMU koos funktsioonidega nagu Laiendatud Lehekülje Tabelid (EPT) virtualiseerimiseks, pakkudes lisakihti aadersside teisendamiseele ja mälu kaitsmisele.
	Segmenteerimine ja lehekülgeda poolt sisse toodud keerukus on tavaliselt OS-i poolt abstraheeritud, pakkudes rakendusetele järjestikust loogilist aadressiruumi.

Segmenteerumine koos lehekülgedega MULTICS süsteemis
	Eelised:
		vähendab välist fragmenteerumist, kasutadessegmentide sees lehekülgedeks jagamist.
		Lihtsustas mäluhaldust, võimaldades programmidel tegeleda loogiliste segmentidega füüsiliste mälupiirangutega tegelemise asemel.
		Parandas turvalisust ja usaldusväärsust, kuna igal segmendil võisid olla oma kaitse seaded ning lehekülgi sai vahetada sisse ja välja, mõjutamata segmentide loogilist struktuuri.
	Keerukus ja lisakulud
		kuigi võimas, tõi see mäluhaldusskeem kaasa keerukust. OS pidi haldama nii segmenditabeleid kui ka leheküljetabeleid, suurendades samme, mis olid vajalikud loogiliste aadresside füüsilisteks aadressideks teisendamiseks.
	Pärand
		MULTICS-süsteemis algatatud kontseptsioonid on mõjutanud kaasaegseid OS-e. Kuigi puhas segmenteerimine on tänapäeval vähem levinud, elab segmenteerimise ja lehekülgedeks jagamise kombinatsiooni pärand edasi, eriti viisil, kuidas mäluhaldust kaasaegsetele rakendusprogrammeerijatele abstraktselt esitatakse.