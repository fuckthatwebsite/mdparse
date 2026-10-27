# MarkdownParser

En lättviktig JavaScript-parser som hämtar en eller flera Markdown-fil(er), omvandlar innehållet till HTML och renderar det i angivet element på sidan.

## Funktioner

- Rubriker (`#` till `######`)
- Stycken
- Punktlistor och numrerade listor
- Enkla tabeller
- Bilder och länkar
- Fet, kursiv och genomstruken text
- Understruken text
- Klassad text med syntaxen `:klass text:`
- Mätning av hämtningstid och parsertid i webbläsarens konsol
- Avbryter pågående hämtningar när sidan lämnas

## Installation

Lägg parserkoden i en fil med `mdparse.js` och ladda den i HTML-dokumentet:

```html
<script src="mdparse.js"></script>
```

Parsern startar automatiskt när dokumentet har laddats.

## Användning

Som standard letar parsern efter element med attributet `data-md-src`. Attributets värde ska vara sökvägen till Markdown-filen:

```html
<div data-md-src="docs/intro.md"></div>

<script src="markdown-parser.js"></script>
```

När sidan laddas hämtar parsern exempelvis `docs/intro.md`, omvandlar innehållet till HTML och infogar resultatet i `<div>`-elementet.

Du kan använda flera element på samma sida:

```html
<div data-md-src="docs/intro.md"></div>
<div data-md-src="docs/guide.md"></div>

<script src="markdown-parser.js"></script>
```

## Markdown-exempel

```markdown
# Välkommen

Det här är ett **fetstilt** ord och det här är *kursivt*.

- Första punkten
- Andra punkten

1. Första steget
2. Andra steget

[Öppna dokumentet](https://example.com)

![Alternativ text](images/example.png)

| Namn | Värde |
| --- | --- |
| En | 1 |
| Två | 2 |

:notice Viktig information:
```

## Förutsättningar och begränsningar

- Sidan och Markdown-filen behöver normalt laddas via en webbserver. `fetch()` fungerar vanligtvis inte när HTML-filen öppnas direkt med `file://`.
- Om Markdown-filen ligger på en annan domän måste servern tillåta hämtningen med CORS.
- Länkar med prefixet `ext ` får `target="_blank"`. Exempel: `[Sök](ext https://example.com)` utöver `target="_blank"` attributet.

## Säkerhet

Parsern tillåter HTML i Markdown och infogar det renderade resultatet med `innerHTML`. Det kan innebära risk för cross-site scripting (XSS) om Markdown-filen innehåller obetrott innehåll. Använd endast betrodda Markdown-filer eller sanera med exempelvis DOMPurify.
