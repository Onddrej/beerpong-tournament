# Beerpong turnaj

Jednosúborová appka na vedenie beerpongového turnaja na **dvoch stoloch** — od zápisu tímov cez skupiny až po pavúk a stupienok víťazov.

Celá appka je jeden HTML súbor. Žiadny build, žiadny server, žiadne závislosti — stačí ho otvoriť v prehliadači.

## Rýchly štart

Stiahni `index.html` a otvor ho dvojklikom. To je všetko.

Funguje aj offline a aj na mobile, takže sa dá obsluhovať priamo pri stole.

## Ako to funguje

Turnaj má štyri kroky, ktoré zodpovedajú kartám v hornej lište:

1. **Tímy** — pridáš tímy a klikneš *Rozlosovať*. Tímy sa náhodne rozhodia do skupiny A (stôl 1) a skupiny B (stôl 2).
2. **Skupiny** — každý s každým v rámci skupiny. Appka vygeneruje rozpis aj živú tabuľku.
3. **Pavúk** — postupujú **všetky** tímy, skupiny slúžia len na nasadenie. Vyraďovačka až do finále, plus zápas o 3. miesto.
4. **Výsledky** — stupienok víťazov, finálna tabuľka a exporty.

Počet tímov je ľubovoľný. Ak nevyjde na mocninu dvojky, najlepšie nasadení dostanú v prvom kole voľný žreb.

## Zápis výsledkov

Klikneš na ktorýkoľvek zápas a otvorí sa panel. Pre každý tím zadáš:

- **trafené poháre** — víťaz sa z nich určí automaticky
- **vyfuknutia**

**Remíza** je povolená v skupinách (1 bod pre oboch). V pavúku nie — tam musí byť jasné, kto postupuje.

## Tabuľky a poradie

V skupine sa body prideľujú **3 za výhru, 1 za remízu, 0 za prehru**. Pri rovnosti rozhoduje v poradí: rozdiel pohárov → vzájomný zápas → počet trafených pohárov.

**Finálna tabuľka** sa po dohraní turnaja radí podľa toho, ako ďaleko sa tím dostal v pavúku — nie podľa bodov. Semifinalistov od seba oddelí zápas o 3. miesto.

## Ukladanie

Turnaj sa **ukladá sám po každej zmene** do `localStorage` prehliadača. V hlavičke vidíš čas posledného uloženia. Po zavretí okna aj po reštarte počítača tam všetko zostane.

O dáta prídeš len v anonymnom okne alebo pri vymazaní dát prehliadania. Na dlhšie turnaje preto použi zálohu:

| Export | Na čo |
|--------|-------|
| **TXT** | Čitateľný výpis — tímy, rozpis, tabuľky, pavúk. Na vytlačenie alebo do chatu. |
| **CSV** | Zápasy a štatistiky pre Excel (oddelené bodkočiarkou). |
| **JSON** | Plná záloha turnaja. Dá sa načítať späť tu aj na inom zariadení. |

## Technické poznámky

- Vanilla HTML, CSS a JavaScript v jednom súbore. Žiadny framework.
- Stav turnaja žije v jednom objekte a serializuje sa do `localStorage` pod kľúčom `beerpong-turnaj-v1`.
- Remízy, body a finálne poradie sa **dopočítavajú** zo zapísaných pohárov — neukladajú sa zvlášť. Formát uložených dát je preto spätne kompatibilný.
- Minimalistický čiernobiely dizajn, responzívny, s podporou `prefers-reduced-motion`.
