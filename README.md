# Ecom coach voor Claude

Je persoonlijke e-commerce coach, rechtstreeks in Claude. Werkt in Claude Code, de Claude-app (Desktop en web) en overal waar je connectors kunt toevoegen. Je logt in met je gewone account; de koppeling werkt zolang je abonnement loopt.

## Claude Code

```bash
claude plugin marketplace add kayakrop1304-gif/claude-plugin
claude plugin install ecom-coach@chievers
```

Daarna in Claude Code: `/mcp`, kies `ecom-coach` en log in. Of stel direct een vraag met `/coach waarom verkoop ik niet`.

Liever zonder plugin, alleen de server:

```bash
claude mcp add --transport http ecom-coach https://chievers-coach-production-272c.up.railway.app/mcp
```

## Claude-app (Desktop en web)

Instellingen, Connectors, Custom connector toevoegen. Naam: `Ecom coach`. Adres:

```
https://chievers-coach-production-272c.up.railway.app/mcp
```

Klik op Koppelen, log in met je account, klaar.

## Wat de coach kan

- `vraag_coach`: advies op maat, met bronnen. De coach kent je winkel, cijfers, dossier en fase.
- `mijn_winkel`: wat de coach al van je weet.
- `mijn_gesprekken`: je laatste gesprekken, om er een voort te zetten.
- `zoek_kennis`: losse naslag in de kennisbank.

Alles wat je via Claude vraagt staat ook in je dashboard.

## Beveiliging

- Inloggen gebeurt op onze eigen pagina, nooit in Claude. Claude krijgt een eigen token dat alleen op deze server werkt, een uur geldig is en automatisch wordt vernieuwd.
- Stopt je abonnement, dan stopt de koppeling binnen een minuut en kan Claude geen nieuw token meer halen.
- Koppeling weghalen: in Claude de connector verwijderen, of in je dashboard alle koppelingen intrekken.
