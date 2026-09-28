# gastrosichtbar.ch

Einseitige Website für gastrosichtbar.ch, Stefan Senn, Brunnen SZ.
Dazu unter `beispiel/` eine Musterseite für das Angebot «Website erstellen».
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
img/stefan.jpg      Porträt, Fallback
img/stefan.webp     Porträt, wird von modernen Browsern geladen
img/og.jpg          Vorschaubild für geteilte Links (1200 × 630 px)
favicon.svg         Symbol im Browser-Tab
robots.txt, sitemap.xml
beispiel/           Musterseite «Gasthaus Musterhof» (erfunden), zugleich Vorlage für Kundenseiten
  index.html        Die ganze Seite, inkl. Impressum und Datenschutz im Fuss
  style.css         Eigenes Design; Farben oben in :root, Schriften aus ../fonts/
  favicon.svg       Symbol im Browser-Tab
  img/              Startbild (800/1600 px) und Bild «Über uns», je WebP und JPG
  BILDER.md         Quelle und Lizenz jedes Bildes
```

Die Musterseite hat `noindex` und steht bewusst nicht in `sitemap.xml`.

## Foto ersetzen

Das Porträt ist seit 28.9.2026 das echte Foto von Stefan (Balkon, Brunnen). Zum Austauschen **beide** Dateien ersetzen, gleicher Name, EXIF/GPS vorher entfernen:

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
| Website (Angebote)     | `<!-- 5b · Website -->`        |
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

## Aus der Musterseite eine Kundenseite machen

1. Ordner `beispiel/` in ein neues Repo bzw. auf den Server des Kunden kopieren, dazu die vier
   Schriften aus `fonts/` (samt Lizenzdateien). In `style.css` die Pfade `../fonts/` anpassen,
   z. B. auf `fonts/`, ebenso die `preload`-Links im `<head>` von `index.html`.
2. In `index.html`:
   - Den Hinweis ganz oben (`<!-- Hinweis Beispielseite … -->`, Absatz `.hinweis`) entfernen.
   - `<meta name="robots" content="noindex">` entfernen, `<title>` und `description` anpassen,
     `<link rel="canonical" href="https://…">` mit der Domain des Betriebs ergänzen.
   - Name, Satz unter dem Namen, Adresse, Öffnungszeiten, Wochenmenü (Datum «Woche vom …» und
     Gerichte), Speisekarte, «Über uns» und Anfahrt ersetzen. Genau dieselben Angaben wie auf Google.
   - Telefon und E-Mail als Links: `<a href="tel:+4141…">041 … </a>` und
     `<a href="mailto:…">…</a>`. Beide Knöpfe «Anrufen» auf `tel:…`, «Reservieren» auf den
     Reservationslink bzw. `tel:` oder `mailto:` des Betriebs.
   - Kartenlink: `https://www.openstreetmap.org/?mlat=BREITE&mlon=LAENGE#map=17/BREITE/LAENGE`
     mit den Koordinaten des Betriebs.
   - Impressum und Datenschutz im Fuss mit den Angaben des Betriebs füllen (Inhaber, Rechtsform,
     allenfalls UID), Server-Standort im Datenschutz prüfen.
   - Jahr und Name in der letzten Zeile des Fusses anpassen.
3. Bilder in `img/` ersetzen: gleiche Dateinamen, Startbild 16:9 (1600 und 800 px breit), Bild
   «Über uns» 4:3 (800 px breit), jeweils WebP und JPG, zusammen unter 400 KB. `alt`-Texte
   anpassen und `BILDER.md` nachführen (oder löschen, wenn die Fotos vom Betrieb stammen).
4. Farben in `style.css` unter `:root` an den Betrieb anpassen (Kontrast prüfen). `favicon.svg`
   ersetzen.
5. Prüfen: Lighthouse (Handy), Gedankenstrich-Grep, bei 375 px kein horizontales Scrollen.

## Farben und Schriften

In `css/style.css` ganz oben unter `:root`:

- `--leinen` Hintergrund, `--tinte` Text, `--weinrot` Akzent, `--senf` nur Schmuck (Sterne, Linie)
- `--serif` Überschriften (Fraunces), `--sans` Fliesstext (Source Sans 3)

## Geprüft

- Lighthouse (Handy und Desktop): Leistung 98–100, Barrierefreiheit 100, Best Practices 100, SEO 100
- Keine Anfrage an fremde Server, keine Konsolenfehler, kein horizontales Scrollen bei 375 px
- Gesamtgewicht Startseite rund 105 KB (ohne Vorschaubild)
- Musterseite `beispiel/` (Handy): Leistung 100, Barrierefreiheit 100, Best Practices 100.
  SEO 66, weil `noindex` gewollt ist (einziger Punkt; ohne `noindex` 100)
