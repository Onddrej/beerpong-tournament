# Beerpong turnaj

Jednosúborová appka na vedenie beerpongového turnaja — od nastavenia formátu cez zápis výsledkov až po stupienok víťazov. Päť formátov, 1 až 8 stolov a odhad, dokedy to potrvá.

Celá appka je jeden HTML súbor. Žiadny build, žiadny server, žiadne závislosti — stačí ho otvoriť v prehliadači.

## Rýchly štart

Stiahni `index.html` a otvor ho dvojklikom. To je všetko.

Funguje aj offline a aj na mobile, takže sa dá obsluhovať priamo pri stole.

## Ako to funguje

Turnaj má päť krokov, ktoré zodpovedajú kartám v hornej lište:

1. **Nastavenie** — vyberieš formát, počet stolov (1–8) a odhadneš si, ako dlho to potrvá.
2. **Tímy** — pridáš tímy a klikneš *Rozlosovať*.
3. **Skupiny / Kolá / Tabuľka** — podľa formátu; rozpis zápasov a živá tabuľka.
4. **Pavúk** — vyraďovačka, ak ju formát má.
5. **Výsledky** — stupienok víťazov, finálna tabuľka a exporty.

Počet tímov je ľubovoľný. Ak nevyjde na mocninu dvojky, najlepšie nasadení dostanú v prvom kole voľný žreb.

## Formáty turnaja

| Formát | Ako funguje | Sedí na |
|--------|-------------|---------|
| **Jedna skupina** | Všetci proti všetkým, vyhráva najlepšia tabuľka. Bez vyraďovačky. | do 8 tímov |
| **Skupiny + pavúk** | 2–4 skupiny každý s každým, potom postupujú všetci do pavúka. | 8–16 tímov |
| **Rovno pavúk** | Bez skupín, hneď vyraďovačka. Jedna prehra a koniec. | keď je málo času |
| **Dvojitá eliminácia** | Dva pavúky — kto prehrá hore, padá do spodného. Koniec až po druhej prehre. | 6–12 tímov |
| **Švajčiarsky systém** | Pevný počet kôl, nikto nevypadáva, súper podľa bilancie. Bez opakovaných zápasov. | 12+ tímov |

Formát sa dá meniť, kým nerozlosuješ. Potom sa zamkne, aby sa nerozbil rozohraný turnaj.

## Stoly

Počet stolov (1–8) je nezávislý od počtu skupín. Zápasy, ktoré sa dajú hrať naraz, appka rozhodí na voľné stoly, takže žiaden stôl nestojí, kým iný má rad.

## Odhad trvania

Na karte *Nastavenie* si **naklikáš počet tímov** (rýchle tlačidlá 4–24 alebo ručne), zadáš dĺžku zápasu a prestávku medzi kolami. Nemusíš mať pridaný ani jeden tím — odhad si vieš pozrieť dopredu a porovnať formáty.

Appka dopočíta počet zápasov, kôl a hlavne **koľko zápasov musí jeden stôl odohrať za sebou** — to je to, čo turnaj naozaj naťahuje. Odhad neráta rozohrávky ani zdržania.

## Zápis výsledkov

Klikneš na ktorýkoľvek zápas a otvorí sa panel. Pre každý tím zadáš **trafené poháre** — víťaz sa z nich určí automaticky. Podľa nastavení k tomu pribudnú vyfuknutia, strelci a Blowjob King.

**Remíza** je povolená v skupinách a švajčiarskych kolách (1 bod pre oboch). V pavúku nie — tam musí byť jasné, kto postupuje.

## Hráči a individuálne štatistiky

V nastaveniach si vyberáš, či zapisuješ **iba tímy**, alebo **tímy + mená** dvoch hráčov. Pri menách sa odomknú tri voliteľné veci:

| Voľba | Čo pribudne |
|-------|-------------|
| **Vyfuknutia** | Koľkokrát tím vyfúkol loptičku. Funguje aj bez mien hráčov. |
| **Strelci** | Pri zápase zapíšeš, koľko pohárov trafil ktorý hráč. Pribudne tabuľka najlepších strelcov a ich stupienok. |
| **Blowjob King** | K vyfuknutiam sa zapíše, kto ich urobil. Kto ich má najviac, je Blowjob King. |

Pravidlo vyfuknutia: keď sa loptička roztočí v poháriku a ešte sa nedotkla piva, súper ju smie vyfúknuť — pohár sa potom neráta.

Hráči nemôžu mať dokopy viac pohárov ani vyfuknutí, než tím v danom zápase naozaj mal; appka to nepustí ďalej. Nechať časť nepriradenú sa dá — tabuľka to vtedy poznámkou prizná.

## Tabuľky a poradie

Body sa prideľujú **3 za výhru, 1 za remízu, 0 za prehru**. Pri rovnosti rozhoduje v poradí: rozdiel pohárov → vzájomný zápas → počet trafených pohárov.

**Finálna tabuľka** sa pri formátoch s pavúkom radí podľa toho, ako ďaleko sa tím dostal — nie podľa bodov. Semifinalistov oddelí zápas o 3. miesto; pri dvojitej eliminácii rozhoduje, ako hlboko tím prežil v spodnom pavúku. Pri formátoch bez pavúka je finálne poradie priamo tabuľka.

## Ukladanie

Turnaj sa **ukladá sám po každej zmene** do `localStorage` prehliadača. V hlavičke vidíš čas posledného uloženia. Po zavretí okna aj po reštarte počítača tam všetko zostane.

O dáta prídeš len v anonymnom okne alebo pri vymazaní dát prehliadania. Na dlhšie turnaje preto použi zálohu:

| Export | Na čo |
|--------|-------|
| **TXT** | Čitateľný výpis — tímy, rozpis, tabuľky, pavúk. Na vytlačenie alebo do chatu. |
| **CSV** | Zápasy, tímové štatistiky a (pri zapnutých strelcoch) aj hráči — pre Excel, oddelené bodkočiarkou. |
| **JSON** | Plná záloha turnaja. Dá sa načítať späť tu aj na inom zariadení. |

## Technické poznámky

- Vanilla HTML, CSS a JavaScript v jednom súbore. Žiadny framework.
- Stav turnaja žije v jednom objekte a serializuje sa do `localStorage` pod kľúčom `beerpong-turnaj-v1`.
- Remízy, body a finálne poradie sa **dopočítavajú** zo zapísaných pohárov — neukladajú sa zvlášť. Formát uložených dát je preto spätne kompatibilný.
- Turnaje uložené pred pridaním formátov nemajú `config`; pri načítaní sa doplní na pôvodné správanie (skupiny + pavúk, 2 skupiny, 2 stoly), takže fungujú ďalej bez zásahu.
- Minimalistický čiernobiely dizajn, responzívny, s podporou `prefers-reduced-motion`.
