# Luiz Air

![Luiz Air preview](assets/luiz-air-preview.png)

Luiz Air is een speelse, interactieve luchtvaartsite met meerdere HTML-pagina’s, afbeeldingen, geluiden en video’s.  
De site bevat onder andere cockpit-achtige schermen, waarschuwingen, vliegtuigthema’s, radar/surveillance-achtige pagina’s en diverse media-effecten.

Dit project is vooral bedoeld als creatieve webpagina / hobbyproject en draait als statische website via Nginx in Docker.

## Inhoud

De site bestaat uit meerdere losse HTML-pagina’s, waaronder:

- `index.html` — hoofdsite / startpagina
- `game.html` — spelpagina
- `luiz.html` — Luiz Air pagina
- `decoder.html` — decoder / encryptie pagina
- `security.html` — security / toegangspagina
- `tracker.html` — tracker pagina
- `surveillance.html` — surveillance pagina
- `wargames.html` — wargames thema
- `intel-signals.html` — intelligence/signals pagina
- `deep-intelligence.html` — extra intelligence pagina
- `rus.html` — themapagina

Daarnaast bevat het project veel afbeeldingen, geluiden en video’s die direct door de HTML-pagina’s worden gebruikt.

## Projectstructuur

Globaal:

```text
.
├── index.html
├── game.html
├── luiz.html
├── security.html
├── tracker.html
├── surveillance.html
├── decoder.html
├── Dockerfile
├── docker-compose.yml
├── sounds/
│   └── *.mp3
├── *.png
├── *.jpg / *.jpeg
├── *.mp3
└── *.mp4

cat > README.md <<'EOF'
# Luiz Air

Luiz Air is een speelse, interactieve luchtvaartsite met meerdere HTML-pagina’s, afbeeldingen, geluiden en video’s.  
De site bevat onder andere cockpit-achtige schermen, waarschuwingen, vliegtuigthema’s, radar/surveillance-achtige pagina’s en diverse media-effecten.

Dit project is vooral bedoeld als creatieve webpagina / hobbyproject en draait als statische website via Nginx in Docker.

## Inhoud

De site bestaat uit meerdere losse HTML-pagina’s, waaronder:

- `index.html` — hoofdsite / startpagina
- `game.html` — spelpagina
- `luiz.html` — Luiz Air pagina
- `decoder.html` — decoder / encryptie pagina
- `security.html` — security / toegangspagina
- `tracker.html` — tracker pagina
- `surveillance.html` — surveillance pagina
- `wargames.html` — wargames thema
- `intel-signals.html` — intelligence/signals pagina
- `deep-intelligence.html` — extra intelligence pagina
- `rus.html` — themapagina

Daarnaast bevat het project veel afbeeldingen, geluiden en video’s die direct door de HTML-pagina’s worden gebruikt.

## Projectstructuur

Globaal:

```text
.
├── index.html
├── game.html
├── luiz.html
├── security.html
├── tracker.html
├── surveillance.html
├── decoder.html
├── Dockerfile
├── docker-compose.yml
├── sounds/
│   └── *.mp3
├── *.png
├── *.jpg / *.jpeg
├── *.mp3
└── *.mp4
Lokaal draaien met Docker

Start de site met Docker Compose:

docker compose up -d --build

Controleer of de container draait:

docker compose ps

Open daarna de site in je browser. Afhankelijk van de poort in docker-compose.yml, bijvoorbeeld:

http://localhost:8080

of vanaf een andere machine:

http://<server-ip>:<poort>
Stoppen
docker compose down
Bestanden die niet in Git staan

Grote mediabestanden kunnen bewust buiten Git blijven, bijvoorbeeld video’s groter dan 100 MB.
GitHub accepteert standaard geen bestanden groter dan 100 MB.

Controleer grote bestanden met:

find . -type f -not -path "./.git/*" -size +90M -exec ls -lh {} \;

Als grote bestanden lokaal nodig zijn, plaats ze handmatig terug in de projectmap.

GitHub

Deze repo bevat de bronbestanden van de Luiz Air site.

Eerste keer pushen:

git remote add origin git@github.com:stefanv2/luiz-air.git
git branch -M main
git push -u origin main

Bij bestaande remote:

git remote -v
git push
Ontwikkeling

Na wijzigingen:

git status
git diff

Wijzigingen committen:

git add .
git commit -m "Update Luiz Air site"
git push
Let op

Dit is een statische hobby-/demo-site. Eventuele wachtwoordvelden, pincodes of “security”-schermen in de HTML zijn niet bedoeld als echte beveiliging. Alles wat in HTML, CSS of JavaScript staat, is zichtbaar voor bezoekers via de browser.

Voor echte beveiliging is server-side authenticatie nodig.

Licentie

Privé/hobbyproject van Stefan Voorbij.
