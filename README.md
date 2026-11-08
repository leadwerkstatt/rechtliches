# Leadwerkstatt – Rechtliche Informationen

Statische Übergangs-Website mit AGB, Impressum und Datenschutzerklärung.
Reines HTML und CSS, kein Build, kein JavaScript, keine Cookies, keine externen Ressourcen.

## Struktur

```
index.html              Startseite
agb/index.html          AGB (Lead Portal + Solar)
impressum/index.html    Impressum
datenschutz/index.html  Datenschutzerklärung
assets/style.css        Gesamtes Styling (Farben, Abstände, Radien als Variablen in :root)
.nojekyll               Schaltet Jekyll auf GitHub Pages ab
```

Der Ordner `quelltexte/` und der Ordner `intern/` stehen in `.gitignore` und werden nicht veröffentlicht.

## Lokal ansehen

`index.html` per Doppelklick im Browser öffnen. Alle Links verweisen bewusst auf `…/index.html`, damit die
Navigation auch lokal ohne Webserver funktioniert.

## Veröffentlichen mit GitHub Pages

1. **Repo anlegen:** In der GitHub-Organisation *New repository*, Name z. B. `rechtliches`.
   Hinweis: GitHub Pages setzt hier ein **öffentliches** Repo voraus. Alles im Repo ist damit öffentlich sichtbar.
   Leer anlegen (ohne README, ohne `.gitignore`, ohne Lizenz).
2. **Vor dem Livegang:** `grep -rn 'PRÜFEN' .` im Projekt ausführen und **alle Treffer klären**
   (die vier gelb markierten Platzhalter in `datenschutz/index.html`). Die Platzhalter im HTML danach
   samt `<mark class="platzhalter">` durch den endgültigen Text ersetzen.
3. **Pushen** (im Projektordner):
   ```
   git remote add origin https://github.com/<ORGANISATION>/<REPO>.git
   git push -u origin main
   ```
4. **Pages aktivieren:** Repo → *Settings* → *Pages* → *Build and deployment* → *Source:* **Deploy from a branch**
   → Branch **main**, Ordner **/ (root)** → *Save*.
5. Nach ein bis zwei Minuten ist die Seite erreichbar unter
   `https://<ORGANISATION>.github.io/<REPO>/`. Der AGB-Link für Kunden ist dann
   `https://<ORGANISATION>.github.io/<REPO>/agb/`.

## Später: eigene Domain verbinden

1. Im Repo-Root eine Datei `CNAME` anlegen, Inhalt nur die Domain, z. B. `recht.leadwerkstatt.de`
   (oder über *Settings → Pages → Custom domain* eintragen, GitHub legt die Datei dann selbst an).
2. DNS-Einträge beim Domain-Anbieter:
   - **Subdomain** (empfohlen, z. B. `recht.`): ein `CNAME`-Eintrag `recht` → `<ORGANISATION>.github.io`
   - **Hauptdomain (Apex)**: vier `A`-Einträge auf `185.199.108.153`, `185.199.109.153`,
     `185.199.110.153`, `185.199.111.153` (optional dazu `AAAA`-Einträge laut GitHub-Dokumentation).
     Die aktuellen Werte vor dem Eintragen in der GitHub-Doku zu „Managing a custom domain for your GitHub Pages site“ gegenprüfen.
3. In *Settings → Pages* die Domain prüfen lassen und, sobald das Zertifikat bereitsteht,
   **Enforce HTTPS** aktivieren.
4. Weil alle Links relativ sind, ist keine Anpassung im Code nötig.
5. Wenn die Seite indexiert werden soll: `<meta name="robots" content="noindex">` in allen vier HTML-Dateien entfernen.
6. Die Datenschutzerklärung nennt GitHub Pages als Hoster. Beim Wechsel des Hostings Text anpassen.

## Branding anpassen

Alle Farben, Abstände und Radien stehen am Anfang von `assets/style.css` im Block `:root`
(dunkler Modus im Block `@media (prefers-color-scheme: dark)` darunter).
