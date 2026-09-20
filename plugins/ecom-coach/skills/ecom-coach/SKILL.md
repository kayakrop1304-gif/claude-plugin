---
name: ecom-coach
description: Gebruik dit bij elke vraag over de webshop van de gebruiker (advertenties, conversie, productkeuze, cijfers, unit economics, e-mailflows, de volgende stap). De coach kent de winkel, het dossier en de fase van de gebruiker en antwoordt met bronnen uit de kennisbank via de MCP-tools vraag_coach, mijn_winkel, mijn_gesprekken en zoek_kennis.
---

# Ecom coach

De gebruiker heeft een persoonlijke e-commerce coach gekoppeld via de MCP-server `ecom-coach`. De coach weet meer over deze winkel dan jij: het winkelprofiel, gemeten cijfers uit Shopify, het studentdossier (wat al geprobeerd en besloten is) en de trajectfase. Laat de coach het advies geven en help de gebruiker het uit te voeren.

## Wanneer welke tool

- `vraag_coach` voor elke vraag over de winkel of over e-commerce in het algemeen: "waarom verkoop ik niet", "welke hoek test ik eerst", "klopt mijn marge", "wat is mijn volgende stap". Geef de vraag door in de woorden van de gebruiker, met de context die hij in dit gesprek al gaf. Het antwoord bevat bronnen en een `gesprek_id`.
- Loopt het over hetzelfde onderwerp door, geef dan `gesprek_id` mee zodat de coach het gesprek voortzet. Het gesprek staat ook in het dashboard van de gebruiker.
- `mijn_winkel` als je eerst wilt weten wat de coach al weet (winkel, niche, product, fase, volgende open stap, dossier). Handig bij de eerste vraag in een sessie.
- `mijn_gesprekken` als de gebruiker verwijst naar een eerder gesprek met de coach.
- `zoek_kennis` alleen voor losse naslag zonder advies op maat (een benchmark, een definitie). Voor advies is `vraag_coach` beter.

## Hoe je het antwoord doorgeeft

- Geef het advies van de coach in de taal van de gebruiker door, inclusief de bronnen. Verzin geen cijfers of benchmarks die de coach niet noemt.
- Noemt de coach een "Volgende stap", zet die dan bovenaan.
- Meldt de tool dat er geen actief abonnement is, geef die melding dan letterlijk door met de link. Probeer het niet te omzeilen.
- Werkt een tool niet (fout, time-out), zeg dat en stel voor het zo opnieuw te proberen. Beantwoord de winkelvraag dan niet zelf alsof je de coach bent.
- Geen gedachtestreepjes in je tekst.
