# Ecom coach voor Claude

Je persoonlijke e-commerce coach, rechtstreeks in Claude. Werkt in claude.ai, de desktop-app en Claude Code. Je logt in met je gewone account; de koppeling werkt zolang je abonnement loopt.

Je koppelt Chief met de plugin `ecom-coach`. De plugin brengt zijn eigen koppeling (connector) mee. Per account werken twee koppelingen tegelijk, bijvoorbeeld Chief in claude.ai en de plugin in Claude Code. Een derde login vervangt de oudste.

## Installeren via claude.ai (aanbevolen)

1. Open [Customize > Plugins](https://claude.ai/customize/plugins) in claude.ai of in de desktop-app.
2. Kies Add > Add marketplace en vul in: `kayakrop1304-gif/claude-plugin`.
3. Kies de plugin `ecom-coach` en klik op Add.
4. Open de plugin, tab Connectors, en verbind `ecom-coach`: log in met je account.

De plugin staat daarna ook in Claude Code en in de Code-tab van de desktop-app, met dezelfde koppeling. Zie je hem daar nog niet, typ dan `/reload-plugins` of start Claude Code opnieuw. Ziet je Claude daar geen Chief-tool die op `scan_start` eindigt (een Chief-connector die je eerder in claude.ai toevoegde, kan een oude lijst tools hebben), log dan één keer in: typ `/mcp`, kies `plugin:ecom-coach:ecom-coach`, kies Authenticate en log in met je Chief-account.

## Alleen Claude Code

Gebruik je geen claude.ai, installeer de plugin dan vanuit Claude Code:

```bash
claude plugin marketplace add kayakrop1304-gif/claude-plugin
claude plugin install ecom-coach@chievers
```

Daarna in Claude Code: `/mcp`, kies `ecom-coach` en log één keer in. Of stel direct een vraag met `/coach waarom verkoop ik niet`.

## Bijwerken

Ga er niet van uit dat een nieuwe versie vanzelf binnenkomt: dat hangt af van je instellingen. Voor `/ecom-coach:concurrentiescan` heb je versie 1.3.0 of nieuwer nodig (sinds 1.3.0 scant hij de hele niche). Kent Claude die opdracht niet, dan heb je nog een oudere versie. Zo werk je bij:

- claude.ai of de desktop-app: open Customize > Plugins, haal `ecom-coach` weg en voeg hem opnieuw toe uit de marketplace `kayakrop1304-gif/claude-plugin`. Verbind daarna de connector opnieuw (tab Connectors).
- Claude Code:

  ```bash
  claude plugin marketplace update chievers
  claude plugin update ecom-coach@chievers
  ```

  Met `claude plugin list` zie je welke versie je hebt.

  Start Claude Code daarna opnieuw, of typ `/reload-plugins`.

## Concurrentiescan

Typ `/ecom-coach:concurrentiescan`. Wil je bepaalde concurrenten er zeker bij, geef ze mee: `/ecom-coach:concurrentiescan concurrent-a.nl concurrent-b.nl`. Het domein van je eigen winkel kun je meegeven met `eigen:jouw-winkel.nl`.

Een scan is altijd een scan van de hele niche, nooit van een paar winkels. Je eigen Claude zoekt met jouw Brandsearch alle Meta-ads in je niche op zoektermen (in de taal van je markt), haalt daarna van de 15 grootste merken alle ads op, stuurt alles naar Chief en labelt de sterkste 400 concepten. Ook haalt hij hun winkelgegevens op (prijzen, garantie, retour, verzending) voor Jij tegen 5. Chief rekent uit wat nu schaalt, wat een oude winnaar is en waar kansen liggen, en zet alles in de tab Concurrenten.

Wat je nodig hebt:

- De plugin met de Chief-koppeling (zie hierboven).
- Brandsearch als connector op je eigen Claude-account: claude.ai, Customize > Connectors. Je hebt een Brandsearch-abonnement met API-tegoed nodig. Nog geen account? Maak er een via https://app.achieversecom.com/brandsearch.
- Een computer met Claude Code of de Code-tab van de desktop-app. Op je telefoon en in een gewone chat werkt de scan niet, want Claude stuurt de bestanden met `curl` naar Chief.
- Plugin versie 1.3.0 of nieuwer (zie Bijwerken).

Claude stelt eerst je markt en 6 tot 20 zoektermen voor (productwoorden en probleemwoorden). Klopt dat, zeg ja of pas de zoektermen aan. Daarna gaat alles vanzelf. Chief rondt een scan pas af als de hele niche is afgezocht: minstens 6 zoektermen, elke zoekterm tot de laatste pagina (hooguit 20 pagina's van 100 ads).

Toestemming: Claude vraagt een paar keer toestemming voor Brandsearch en Chief: kies Altijd toestaan (in de terminal heet dat "Yes, and don't ask again"). Gaat een vraag over iets anders dan Brandsearch, Chief, de winkels van je concurrenten of de map `chief-scan`, kies dan Nee.

Gestopt? Draai `/ecom-coach:concurrentiescan` opnieuw: Chief pakt je open scan op. Je Claude haalt dan geen ads opnieuw op en gaat verder waar hij was, bijvoorbeeld met labelen. Dat kan tot 72 uur na de start van de scan. Wil je bewust opnieuw beginnen, typ dan `/ecom-coach:concurrentiescan nieuw`, eventueel met domeinen erachter. De oude scan stopt dan.

Log niet op een derde plek opnieuw in bij Chief zolang de scan loopt. Per account werken twee koppelingen tegelijk: een derde login vervangt de oudste, en dan kan de scan stoppen. Hij blijft wel open staan: log in Claude Code opnieuw in (`/mcp`) en zeg in hetzelfde gesprek "ga door", of draai de opdracht later opnieuw.

Kosten: de scan gebruikt het tegoed van je eigen Brandsearch-account. Dat is 1 aanroep per pagina van 100 ads: hooguit 20 pagina's per zoekterm, en daarna hooguit 11 per groot merk. Reken op 150 tot 600 aanroepen; met minder dan 100 begint Claude er niet aan. Merken opzoeken is gratis. Een scan heeft hooguit 11.000 ads. Daarna labelt je eigen Claude de sterkste 400 concepten (op looptijd, varianten en bereik): hooguit 16 rondes van 25 per gesprek, plus een paar controlevragen waarmee Chief nagaat of de labels kloppen. De andere concepten tellen mee in de totalen en de merken. Dat kost een flink deel van je Claude-limiet en duurt al snel een tot twee uur. Chief rondt af zodra 80 procent van die sterkste concepten een label heeft. Lukt dat niet in één gesprek, dan stopt Claude na 16 rondes en zegt wat je kunt doen: draai de opdracht later opnieuw om verder te labelen.

Je Claude stuurt de ruwe ads en winkelpagina's van je concurrenten naar Chief. Chief bewaart de adtekst hooguit 72 uur. Daarna blijven alleen labels, cijfers en een korte kop over.

## Wat de coach kan

Je eigen Claude schrijft het advies. De coach levert per vraag een briefing: wat hij van je winkel, cijfers, dossier en fase weet, plus de kennis uit de kennisbank die bij je vraag hoort. Hoe beter het model dat je in Claude kiest, hoe beter het advies.

- `vraag_coach`: de briefing voor je vraag.
- `lees_kennis`: een hele kennispagina uit de briefing lezen.
- `zoek_kennis`: gericht verder zoeken in de kennisbank.
- `rond_af`: het antwoord vastleggen in je dashboard, zodat de coach onthoudt wat er besproken is.
- `mijn_winkel`: wat de coach al van je weet.
- `mijn_gesprekken`: je laatste gesprekken, om er een voort te zetten.
- `scan_start`, `scan_nieuw_token`, `scan_concepten`, `scan_labels`, `scan_klachten`, `scan_klaar`: de stappen van de concurrentiescan.
- `mijn_concurrenten`: de uitkomst van de laatste afgeronde scan van je actieve winkel, zodat Claude er hooks en scripts mee kan schrijven. Heeft die winkel nog geen scan, dan zegt Chief dat; een scan van een andere winkel krijg je nooit.

Alles wat je via Claude vraagt staat ook in je dashboard.

## Beveiliging

- Inloggen gebeurt op onze eigen pagina, nooit in Claude. Claude krijgt een eigen token dat alleen op deze server werkt, een uur geldig is en automatisch wordt vernieuwd.
- Voor de concurrentiescan krijgt Claude een apart scantoken. Dat werkt alleen voor het uploaden van scanbestanden en verloopt na 60 minuten.
- Stopt je abonnement, dan stopt de koppeling binnen een minuut en kan Claude geen nieuw token meer halen.
- Per account werken twee Claude-koppelingen tegelijk: een derde vervangt de oudste. Je login delen met iemand anders zet dus jezelf buiten spel.
- De concurrentiescan leest tekst van concurrenten, en daar kan een opdracht in staan. Daarom mag `/ecom-coach:concurrentiescan` zonder te vragen alleen de scantools van Chief gebruiken, uploaden naar het adres van Chief, winkelpagina's ophalen naar de map `chief-scan` en bestanden schrijven in die map. Die toestemmingsregels alleen zijn geen harde grens: een regel die met het adres van Chief begint, laat achter dat begin ook een extra adres of een ander bestand toe.
- Daarom komt er een extra slot mee: de Chief-scanwacht. Die controleert elke scanopdracht via Bash, Monitor of PowerShell: elke opdracht die `curl` aanroept en de map `chief-scan/` of het uploadadres van Chief (`concurrenten/upload`) noemt. Zo'n opdracht moet precies de vaste vorm hebben: één adres, en dat is het uploadadres van Chief of een vaste pagina van een winkel; opslaan alleen in `chief-scan`; niets ervoor of erachter, geen `$`, backticks, `;` of `|`. Wijkt hij af, dan houdt Claude Code hem tegen. In Bash en Monitor geldt dat ook als de `curl` achter een andere opdracht staat (`ls chief-scan/ && curl ...`); de reden zegt dan waarom hij als scanopdracht telt.
- Noemt een opdracht in Bash of Monitor `chief-scan/` of `concurrenten/upload`, dan houdt de wacht ook elke `$( )`, backtick of procesvervanging (`<( )`, `>( )`) erin tegen, ook tussen aanhalingstekens en in een commitbericht. Een `curl` kan zich daarin verstoppen. Schrijf zo'n commitbericht bijvoorbeeld met `git commit -F bestand`.
- Met rust laat de wacht: een gewone `curl` zonder die twee, en één losse `grep`, `echo`, `printf`, `cat`, `head`, `tail`, `ls`, `wc` of `git commit` die `curl` alleen als tekst noemt, zonder `;`, `|`, `&`, `<`, `>`, haakjes, accolades of een nieuwe regel.
- Al het andere vraagt Claude Code eerst aan jou, tenzij je Claude Code zelf ruimer hebt ingesteld (bijvoorbeeld een modus die alles zonder vragen toestaat, of een eigen regel die elke `curl` toestaat). Twijfel je bij een vraag, kies dan Nee.
- Wat de wacht niet is: een waterdichte grens.
  - Kan de wacht niet starten of is hij niet op tijd klaar, dan laat Claude Code de opdracht door en beslissen alleen de toestemmingsregels.
  - Getest op macOS. Op Windows (Git Bash en de PowerShell-wacht) is hij nog niet getest.
  - Een upload mag elk opgeslagen toolresultaat van Claude Code versturen (de map `tool-results` van al je gesprekken, niet alleen dit gesprek), maar alleen naar Chief.
  - Een winkelpagina controleert de wacht alleen op vorm: hij weet niet welke merken je bevestigde. Een vaste pagina van een ander domein ophalen kan dus, en de naam van dat domein kan zelf gegevens uit het gesprek meenemen (`https://<gegevens>.voorbeeld.com/meta.json`). Bestanden van jou gaan zo niet mee.
  - Heb je op macOS of Linux zelf de PowerShell-tool aangezet, dan controleert de wacht die niet.
- Nog open, keuze van de beheerder: winkelpagina's alleen van bevestigde merken toestaan. Dat kan op drie manieren: (1) de wacht leest de bevestigde domeinen uit het laatste antwoord van `scan_start` in het gesprek; (2) een hook van type `http` laat Chief het domein toetsen aan de merken van de scan (die laat de opdracht door als Chief onbereikbaar is); (3) de regel voor winkelpagina's uit het commando halen, dan vraagt Claude Code bij elke winkelpagina om toestemming. En voor een release: de wacht één keer draaien op een Windows-machine.
- Koppeling weghalen: in Claude de connector verwijderen, of in je dashboard alle koppelingen intrekken.
