# FameLive PWA – iPhone-Version

## Was funktioniert?
- Private Kameravorschau (Front-/Rückkamera), Mikrofon, simulierte Zuschauer, Kommentare, Likes, Geschenke und Statistiken.
- Aufnahme des Kamera-/Mikrofonstreams, sofern Safari `MediaRecorder` unterstützt; Aufnahmen in IndexedDB und über das iOS-Teilen-Menü exportierbar.
- Nach dem ersten HTTPS-Aufruf mit geladenem Service Worker offline nutzbar. Keine Server-API, keine echten Zuschauer, keine Abos.

## Wichtige Grenzen
- Die ZIP-Datei **kann auf dem iPhone nicht einfach durch Antippen als PWA gestartet werden**: iOS-Safari benötigt für Kamera und Service Worker eine **HTTPS-Adresse**. `file://` ist dafür ungeeignet.
- Du musst die entpackten Dateien einmal bei einem statischen HTTPS-Host bereitstellen (z.B. GitHub Pages, Netlify Drop oder Cloudflare Pages). Das Hosting stellt nur die Dateien bereit, verarbeitet keine Videos. Einmal geladen und zum Home-Bildschirm hinzugefügt, läuft die App auch offline.
- `MediaRecorder` und MP4/WebM-Codec-Unterstützung variieren je nach iOS-Version. Aufnahmen können bei wenig Speicher fehlschlagen. Der Export enthält das Kameravideo mit Ton, **nicht** die Chat-Overlays.
- Bei App-Wechsel wird der simulierte Stream beendet, damit die Kamera nicht unbemerkt weiterläuft. iOS kann große lokale Browserdaten selbstständig bereinigen.

## Nur mit iPhone installieren
1. ZIP in der Dateien-App öffnen und entpacken.
2. Alle Dateien aus `famelive-pwa` zu einem statischen HTTPS-Hosting hochladen. Für GitHub Pages: neues öffentliches Repository erstellen, die Dateien ins Stammverzeichnis hochladen, unter Settings → Pages „Deploy from a branch“ wählen (Branch `main`, Ordner `/root`). Dann die angezeigte `https://...github.io/.../` Adresse öffnen. Achtung: Ein öffentliches Repository macht den Quellcode öffentlich; es enthält keine persönlichen Aufnahmen.
3. Die HTTPS-Adresse **in Safari** öffnen.
4. Teilen → „Zum Home-Bildschirm“ → „Hinzufügen“.
5. FameLive vom Home-Bildschirm öffnen, „Live starten“ wählen und Kamera/Mikrofon erlauben.
6. Flugmodus aktivieren, WLAN deaktivieren und erneut öffnen, um Offline-Nutzung nach dem ersten Laden zu prüfen.

## Datenschutz
Videos werden nicht hochgeladen. Ein Hosting-Anbieter sieht technisch die Seitenaufrufe/IP-Adresse beim ersten Laden. Alle simulierten Interaktionen sind lokal. Kein Analytics-SDK.

## Tests
Statische HTML/CSS/JS-Checks und ZIP-Integrität sind möglich; ein tatsächlicher Safari-iPhone-Test wurde in dieser Umgebung nicht durchgeführt.
