# gastrosichtbar.ch

Einseitige Website für gastrosichtbar.ch, Stefan Senn, Brunnen SZ.
Reines HTML und CSS, kein JavaScript, keine externen Einbindungen, keine Cookies.

## Seite lokal ansehen

Am einfachsten: `index.html` im Browser öffnen (Doppelklick).

Mit einem kleinen lokalen Server (empfohlen, verhält sich wie online):

```sh
# im Ordner des Repos
python3 -m http.server 8080
# oder
npx http-server -p 8080
```

Dann im Browser `http://localhost:8080` öffnen.

## Aufbau

```
index.html          Startseite (alle Abschnitte)
impressum.html      Impressum
datenschutz.html    Datenschutzerklärung
css/style.css       Alle Stile; Farben und Schriften oben in :root
fonts/              Selbst gehostete Schriften (Fraunces, Source Sans 3, SIL OFL 1.1)
img/stefan.jpg      Porträt (Platzhalter), Fallback
img/stefan.webp     Porträt (Platzhalter), wird von modernen Browsern geladen
img/og.jpg          Vorschaubild für geteilte Links (1200 × 630 px)
favicon.svg         Symbol im Browser-Tab
robots.txt, sitemap.xml
```

## Foto ersetzen

Das Porträt ist ein Platzhalter. Ersetzen Sie **beide** Dateien, gleicher Name:

- `img/stefan.jpg`
- `img/stefan.webp`

Empfehlung: Oberkörper, Hochformat 4:5, **800 × 1000 px**. Das Bild wird automatisch
auf 4:5 zugeschnitten. WebP erzeugen, z. B. mit

```sh
cwebp -q 78 stefan.jpg -o img/stefan.webp
```

oder online mit squoosh.app (Datei bleibt dabei auf Ihrem Rechner).
Zielgrösse: je unter 100 KB.

Hat das Foto ein anderes Seitenverhältnis, in `index.html` bei `<img src="img/stefan.jpg" …>`
die Werte `width` und `height` anpassen.

## Texte ersetzen

Alle Texte stehen direkt in `index.html`. Jeder Abschnitt ist mit einem Kommentar markiert:

| Abschnitt              | Kommentar in index.html        |
| ---------------------- | ------------------------------ |
| Kopf (Titel, Knöpfe)   | `<!-- 1 · Kopf -->`            |
| Wer                    | `<!-- 2 · Wer -->`             |
| Das Problem            | `<!-- 3 · Das Problem -->`     |
| Beispiel-Bewertung     | `<!-- 4 · Beispiel … -->`      |
| Paket und Preis        | `<!-- 5 · Paket und Preis -->` |
| So läuft es            | `<!-- 6 · So läuft es -->`     |
| Kontakt                | `<!-- 7 · Kontakt -->`         |
| Fuss                   | `<!-- 8 · Fuss -->`            |

Telefonnummer, E-Mail oder Preis kommen mehrfach vor (Knöpfe, Kopf, Kontakt, Meta-Angaben
im `<head>`, strukturierte Daten `application/ld+json`, Unterseiten). Bei einer Änderung
im ganzen Ordner suchen und ersetzen, z. B. nach `768319899`, `831 98 99` und
`stefan@gastrosichtbar.ch`.

Titel und Beschreibung für Suchmaschinen und geteilte Links stehen oben im `<head>`
(`<title>`, `description`, `og:…`). Wenn sich der Titel ändert, auch `img/og.jpg` neu erstellen.

Im Datenschutz ist der Hosting-Anbieter nicht namentlich genannt. Sobald klar ist, wo die
Seite liegt, den Abschnitt «Server-Protokolle» in `datenschutz.html` ergänzen.

## Farben und Schriften

In `css/style.css` ganz oben unter `:root`:

- `--leinen` Hintergrund, `--tinte` Text, `--weinrot` Akzent, `--senf` nur Schmuck (Sterne, Linie)
- `--serif` Überschriften (Fraunces), `--sans` Fliesstext (Source Sans 3)

## Geprüft

- Lighthouse (Handy und Desktop): Leistung 98–100, Barrierefreiheit 100, Best Practices 100, SEO 100
- Keine Anfrage an fremde Server, keine Konsolenfehler, kein horizontales Scrollen bei 375 px
- Gesamtgewicht Startseite rund 105 KB (ohne Vorschaubild)
