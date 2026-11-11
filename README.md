# RÁNO. — raňajkáreň na EF UMB

Kompletný statický web pre školský podnikateľský projekt. Pracovná značka RÁNO., vlastný dizajn, slovenské texty a interaktívny katalóg. Bez objednávok a platieb.

## Najrýchlejšie spustenie

Rozbaľ archív a otvor `index.html` v Safari, Chrome, Edge alebo Firefoxe. Ponechaj pri ňom celý priečinok `assets`. Nie je potrebný Node.js, npm, databáza ani inštalácia balíkov. Na fotografie je potrebné pripojenie na internet.

Samostatne dodaný súbor `RANO-interaktivny-nahlad.html` obsahuje všetky podstránky aj kód v jednom súbore. Otvor ho v bežnom prehliadači, nie v textovom editore alebo v rýchlom náhľade Finderu. Slúži na prezeranie; na GitHub nahraj tento viacstránkový projekt. Aj samostatný náhľad načítava fotografie online.

## Zverejnenie na GitHub Pages

1. Na GitHube vytvor nový **Public** repozitár, napríklad `rano-ranajkaren`.
2. V repozitári zvoľ **Add file → Upload files**. Nahraj **obsah rozbaleného archívu**, nie ZIP a nie nadradený priečinok. `index.html` musí byť priamo v koreni repozitára, spolu s priečinkom `assets`.
3. Skontroluj, že ostala zachovaná štruktúra `assets/css`, `assets/js` a `assets/images`. Potvrď **Commit changes** do vetvy `main`.
4. Otvor **Settings → Pages**. Pri **Source** vyber **Deploy from a branch**. Nastav **main** a **/(root)**, potom **Save**.
5. Keď GitHub dokončí nasadenie, v rovnakej sekcii zobrazí odkaz **Visit site**. Stav je viditeľný aj v záložke Actions.

Príklad formátu adresy, nie už zverejnený web:

```text
https://TVOJE-MENO.github.io/rano-ranajkaren/
```

Na GitHub Free použi verejný repozitár. Do repozitára nepatria heslá, tokeny ani súkromné údaje. Tento projekt žiadne prístupové kľúče nepotrebuje. Na prvé publikovanie nie je potrebná vlastná doména.

Ak sa zobrazí 404, skontroluj umiestnenie `index.html`, zvolenú vetvu a dokončenie publikovania. Ak sa zobrazí len text bez štýlu, nie je správne nahraný priečinok `assets` alebo je vnorený o jednu úroveň hlbšie. Názvy súborov nemeníme na veľké písmená.

Oficiálne podklady, overené 11. 11. 2026:
- https://docs.github.com/en/pages/quickstart
- https://docs.github.com/en/pages/getting-started-with-github-pages/creating-a-github-pages-site

## Čo funguje

- Úvodná stránka, katalóg, detail produktu, o nás, kontakt, informácie o projekte, textový/tlačový jedálny lístok a 404.
- 16 produktov so zložením, cenou, gramážou a navrhnutými alergénmi.
- Kategórie, vyhľadávanie bez citlivosti na diakritiku, vegetariánsky filter, zoradenie a filter obľúbených.
- Rýchly náhľad na počítači aj samostatný detail každého produktu na všetkých zariadeniach.
- Obľúbené položky a raňajkové kombo sa ukladajú v tomto prehliadači. Nejde o účet, objednávku ani databázu.
- Kombo prepočítava jedlo + vybranú kávu so zľavou 0,70 €, aritmetika počíta v centoch.
- Mobilná navigácia, klávesové ovládanie, Escape pri dialógu, viditeľné zaostrenie a rešpektovanie obmedzenia animácií v systéme.
- Kopírovanie adresy/odkazu s náhradným oznámením, ak ho prehliadač zakáže. Externá navigácia a mapa OpenStreetMap načítaná až po kliknutí.
- Bez JavaScriptu ostávajú dostupné hlavné informačné stránky a `menu-prehlad.html`.

## Štruktúra projektu

```text
index.html                 Domov a konfigurátor komba
menu.html                  Interaktívny katalóg
produkt.html               Detail podľa ?id=bagel-losos
o-nas.html                 Koncept raňajkárne
kontakt.html               Adresa, hodiny, mapa, otázky
projekt.html               Označenie projektu, zdroje, súkromie
menu-prehlad.html          Textová a tlačová ponuka
404.html                   Nenájdená stránka
assets/css/style.css       Vizuál a responzívne zobrazenie
assets/js/data.js          Produkty a kategórie
assets/js/app.js           Všetky interaktívne funkcie
assets/js/icons.js         Ikony
assets/images/             Zdrojový zoznam a náhradný obrázok
assets/favicon.svg         Ikona webu
tools/download_photos.py   Voliteľné uloženie fotografií lokálne
```

## Úpravy obsahu

Produkty upravuj v `assets/js/data.js`. Cenu zapisuj ako číslo s bodkou, napríklad `4.2`; web ju sám zobrazí ako `4,20 €`. ID používaj bez medzier a diakritiky. `featured: true` zaraďuje produkt na úvodnú stránku. `pair` je ID odporúčaného doplnku.

Katalóg, produktové detaily a prepočet komba čítajú tieto dáta automaticky. Statická karta croissantu v hero sekcii a `menu-prehlad.html` sú samostatný HTML obsah: pri zmene cien alebo ponuky aktualizuj aj ich. Názov značky, hodiny, texty a navigáciu uprav na všetkých HTML stránkach. Farebné premenné sú na začiatku `style.css`.

Pre lokálne testovanie cez HTTP môžeš v priečinku projektu spustiť `python3 -m http.server 8000` a otvoriť `http://localhost:8000`. Nie je to potrebné na GitHub Pages; ide len o voliteľný vývojový postup.

## Fotografie

Fotografie sú ilustračné z Pexels a Unsplash, nie fotografie skutočnej prevádzky alebo presných receptúr. Načítavajú sa z externých obrazových serverov. Zoznam originálov a autorov na zdrojových stránkach je dostupný cez `assets/images/photo-sources.json`.

Pre nezávislosť od týchto serverov je priložený **voliteľný** skript. S Pythonom 3 a pripojením na internet spusti z priečinka projektu:

```sh
python3 tools/download_photos.py --dry-run
python3 tools/download_photos.py
```

Prvý príkaz iba vypíše použité URL. Druhý stiahne dostupné fotografie do `assets/images/photos/` a zmení ich odkazy v HTML a JavaScripte na lokálne. Pôvodné súbory zálohuje v `.photo-backup/`. Neúspešné odkazy ponechá externé a vypíše chybu; nepredstiera úspešné stiahnutie. Potom nahraj aktualizovaný projekt na GitHub. Samostatný HTML náhľad sa týmto skriptom nemení.

Podmienky zdrojov: https://www.pexels.com/license/ a https://unsplash.com/license

## Dôležité pred prezentovaním

RÁNO. je vymyslená značka pre tento projekt. Ceny, gramáže, otváracie hodiny a alergény sú návrhom. Pri reálnom predaji by bolo potrebné overiť receptúry, dodávateľov, možné stopy alergénov a faktické informácie o prevádzke. Web nie je oficiálnou stránkou UMB. Presné miesto raňajkárne v budove nie je určené.

Výrobný kód neobsahuje analytiku, reklamné skripty ani falošné odosielacie formuláre. GitHub a obrazové/mapové služby sú externí poskytovatelia. Uloženie obľúbených a komba funguje iba tam, kde ho prehliadač povoľuje. Nastavenie `noindex` a `robots.txt` obmedzuje indexovanie školského konceptu, ale nie je zabezpečením alebo ochranou pred verejným prístupom.

Adresa fakulty: https://www.ef.umb.sk/kontakt/adresa-a-fakturacne-udaje.html
Inšpirácia: https://chliebalaska.sk/ ; https://gails.com/collections/breakfast ; https://oleandsteen.us/

## Overenie

V Chromium bolo vykonaných **88 kontrol** interaktívneho náhľadu: všetkých 16 produktov, filtre, vyhľadávanie, zoradenie, dialóg, obľúbené, kombo, mobilné menu, FAQ, neplatné ID a zobrazenie v šírkach 320, 390, 768, 1024 a 1440 px. Bez nezachytených JavaScriptových chýb v testoch. Skontrolované sú aj lokálne odkazy a syntax JavaScriptu.

Testovanie prebehlo v izolovanom prostredí s blokovaným sieťovým prístupom. Preto bolo skontrolované rozloženie a interakcie vrátane náhradného obrázka; skutočné načítanie externých fotografií a mapy, download skriptu a nasadenie na živom GitHub Pages nebolo možné overiť. Pred odovzdaním otvor zverejnenú stránku na počítači aj mobile a skontroluj fotografie, menu, detail a mapu.
