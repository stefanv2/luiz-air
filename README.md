# L.A. LUIZ-AIR & CARGO 🇧🇷

![Luiz Air preview](assets/luiz-air-preview.png)

**L.A. LUIZ-AIR & CARGO** is een speelse en interactieve luchtvaartwebsite met meerdere thema-pagina’s, vliegtuigsimulators, cargo- en VIP-functies, command-center schermen, geluiden, video’s en afbeeldingen.

De site is gebouwd als creatief hobby-/familieproject en draait als statische website via **Nginx in Docker**.

---

## Inhoud

- [Over dit project](#over-dit-project)
- [Belangrijkste pagina’s](#belangrijkste-paginas)
- [Projectstructuur](#projectstructuur)
- [Media-indeling](#media-indeling)
- [Lokaal draaien met Docker](#lokaal-draaien-met-docker)
- [Nieuwe media toevoegen](#nieuwe-media-toevoegen)
- [Git workflow](#git-workflow)
- [Handige controles](#handige-controles)
- [Let op](#let-op)
- [Licentie](#licentie)

---

## Over dit project

Dit project is een verzameling interactieve HTML-pagina’s rondom het fictieve luchtvaartbedrijf **L.A. LUIZ-AIR & CARGO**.

De website bevat onder andere:

- passagiersvluchten
- cargo-vluchten
- VIP-jets
- vliegtuigafbeeldingen
- promotievideo’s
- cockpit- en landing-simulatoren
- command-center dashboards
- security- en surveillance-pagina’s
- geluiden en callouts
- speelse capybara- en vliegtuigthema’s

---

## Belangrijkste pagina’s

### Hoofdpagina

| Bestand | Omschrijving |
|---|---|
| `index.html` | Startpagina van L.A. LUIZ-AIR & CARGO met passagiersvluchten, cargo, VIP-jets, gallery-link, security-link en simulator-link. |

### Simulator en games

| Bestand | Omschrijving |
|---|---|
| `luiz-warning-panel.html` | Landing Career Simulator met hoogte-callouts, landing gear, flaps, master warning, touchdown en score. |
| `game.html` | Speelse gamepagina met vliegtuig- en capybara-thema. |

### Command center / defense pagina’s

| Bestand | Omschrijving |
|---|---|
| `ops-briefing.html` | OPS Briefing Center met weerinformatie, space weather, situation room en live briefingstijl. |
| `tracker.html` | Tactical ETA Tracker met routeplanning, afstand, snelheid en aankomsttijd. |
| `surveillance.html` | Surveillance-dashboard met luchtvaart-, satelliet- en monitoringstijl. |
| `intel-signals.html` | SIGINT / radio / space monitor pagina. |
| `deep-intelligence.html` | Extra intelligence-dashboard met externe informatiebronnen en monitoringpanelen. |
| `security.html` | Security/thema-pagina met command aircraft en beveiligingsstijl. |
| `decoder.html` | Decoder/encryptiepagina. |

### Extra thema’s

| Bestand | Omschrijving |
|---|---|
| `luiz.html` | Extra Luiz-Air promotiepagina. |
| `rus.html` | Thema-pagina met Sovjet/Russische luchtvaartstijl. Staat mogelijk alleen lokaal als deze bewust uit Git is gehaald. |

---

## Projectstructuur

Globaal ziet de repository er zo uit:

```text
.
├── index.html
├── game.html
├── luiz.html
├── luiz-warning-panel.html
├── ops-briefing.html
├── tracker.html
├── surveillance.html
├── security.html
├── intel-signals.html
├── deep-intelligence.html
├── decoder.html
├── Dockerfile
├── docker-compose.yml
├── assets/
│   └── images/
│       └── *.png / *.jpg / *.jpeg / *.webp
├── sounds/
│   └── *.mp3
├── video/
│   └── *.mp4
└── README.md
```

---

## Media-indeling

De media zijn bewust verdeeld over aparte mappen:

| Map | Inhoud |
|---|---|
| `assets/images/` | Afbeeldingen zoals vliegtuigen, logo’s, cockpitbeelden en gallery-afbeeldingen. |
| `sounds/` | Geluiden en mp3-bestanden zoals callouts, cabin beeps en engine sounds. |
| `video/` | Video’s zoals promo-video’s en VIP-jet beelden. |

Hierdoor blijft de hoofdmap overzichtelijk en staan de meeste losse media-bestanden niet meer direct in de root van de repository.

---

## Lokaal draaien met Docker

De website draait als statische Nginx-site.

### Starten

```bash
docker compose up -d --build
```

### Controleren

```bash
docker compose ps
```

### Openen

Lokaal op de Docker-host:

```text
http://localhost:8080
```

Vanaf een andere machine in het netwerk:

```text
http://<server-ip>:8080
```

### Stoppen

```bash
docker compose down
```

---

## Dockerfile

De site gebruikt een eenvoudige Nginx-container:

```dockerfile
FROM nginx:alpine
COPY . /usr/share/nginx/html
EXPOSE 80
```

Omdat de bestanden tijdens de build naar de container worden gekopieerd, moet je na HTML/CSS/JS/media-wijzigingen opnieuw builden:

```bash
docker compose up -d --build
```

---

## Nieuwe media toevoegen

### Nieuwe afbeeldingen

Plaats nieuwe afbeeldingen bij voorkeur in:

```text
assets/images/
```

Gebruik daarna in HTML:

```html
<img src="assets/images/voorbeeld.png" alt="Voorbeeld">
```

Of in JavaScript:

```js
const IMAGE = "assets/images/voorbeeld.png";
```

### Nieuwe geluiden

Plaats nieuwe mp3-bestanden bij voorkeur in:

```text
sounds/
```

Voorbeeld:

```html
<audio src="sounds/voorbeeld.mp3"></audio>
```

### Nieuwe video’s

Plaats video’s bij voorkeur in:

```text
video/
```

Voorbeeld:

```html
<video controls>
  <source src="video/promo.mp4" type="video/mp4">
</video>
```

---

## Git workflow

### Status controleren

```bash
git status
git diff
```

### Alles toevoegen

```bash
git add -A
```

### Commit maken

```bash
git commit -m "Update Luiz-Air site"
```

### Pushen

```bash
git push
```

### Werken met een aparte branch

Voor grotere wijzigingen is een aparte branch handig:

```bash
git checkout -b mijn-wijziging
```

---

## Handige controles

### Zoek root-level afbeeldingen

```bash
find . -maxdepth 1 -type f \( \
  -iname "*.jpg" -o \
  -iname "*.jpeg" -o \
  -iname "*.png" -o \
  -iname "*.webp" \
\) -printf "%f\n" | sort
```

### Zoek root-level mp3-bestanden

```bash
find . -maxdepth 1 -type f -iname "*.mp3" -printf "%f\n" | sort
```

### Zoek root-level mp4-bestanden

```bash
find . -maxdepth 1 -type f -iname "*.mp4" -printf "%f\n" | sort
```

### Controleer oude image-paden

```bash
grep -RInE "['\"][^'\"]+\.(jpg|jpeg|png|webp)(\?[^'\"]*)?['\"]" . \
  --include="*.html" \
  --include="*.css" \
  --include="*.js" \
  --exclude-dir=".git" \
| grep -v "assets/images/" \
| grep -v "http://" \
| grep -v "https://"
```

### Controleer Git whitespace

```bash
git diff --check
```

---

## Let op

Dit is een creatieve hobby-/demo-site. Eventuele security-schermen, pincodes, access panels of waarschuwingen in HTML/JavaScript zijn bedoeld voor spel en beleving.

Alles wat in HTML, CSS en JavaScript staat, is zichtbaar in de browser. Voor echte beveiliging is server-side authenticatie nodig.

---

## Licentie

Privé/hobbyproject van **Stefan Voorbij**.
