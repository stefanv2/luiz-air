# Luiz Air

![Luiz Air preview](assets/luiz-air-preview.png)

L.A. LUIZ-AIR & CARGO 🇧🇷

L.A. LUIZ-AIR & CARGO is een speelse, interactieve luchtvaartwebsite met meerdere pagina’s, vliegtuigthema’s, simulator-elementen, cargo/vip-functies, command-center schermen, geluiden, video’s en afbeeldingen.

Het project is gebouwd als creatieve hobby-/familiesite en draait als statische website via Nginx in Docker.

Wat zit er in deze site?

De site bestaat uit meerdere losse HTML-pagina’s met elk een eigen thema.

Hoofdpagina
index.html
Startpagina van L.A. LUIZ-AIR & CARGO met passagiersvluchten, cargo, VIP-jets, gallery-link, security-link en simulator-link.
Simulator en games
luiz-warning-panel.html
Landing Career Simulator met hoogte-callouts, landing gear, flaps, master warning, touchdown en score.
game.html
Speelse gamepagina met vliegtuig/capybara-thema.
Command center / defense pagina’s
ops-briefing.html
OPS Briefing Center met weerinformatie, space weather, situation room en live briefingstijl.
tracker.html
Tactical ETA Tracker met routeplanning, afstand, snelheid en aankomsttijd.
surveillance.html
Surveillance-dashboard met luchtvaart-, satelliet- en monitoringstijl.
intel-signals.html
SIGINT / radio / space monitor pagina.
deep-intelligence.html
Extra intelligence-dashboard met externe informatiebronnen en monitoringpanelen.
security.html
Security/thema-pagina met command aircraft en beveiligingsstijl.
decoder.html
Decoder/encryptiepagina.
Extra thema’s
luiz.html
Extra Luiz-Air promotiepagina.
rus.html
Thema-pagina met Sovjet/Russische luchtvaartstijl.
Let op: als deze lokaal bewust uit Git is gehaald, staat hij mogelijk niet meer in de GitHub-repo.
Projectstructuur

Globaal ziet de repo er zo uit:

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
Media

De media zijn bewust verdeeld over aparte mappen:

assets/images/   afbeeldingen
sounds/          geluiden / mp3-bestanden
video/           video-bestanden

Hierdoor blijft de hoofdmap overzichtelijk en staan de meeste losse bestanden niet meer direct in de root van de repository.

Lokaal draaien met Docker

De site draait als statische Nginx-site.

Starten:

docker compose up -d --build

Controleren:

docker compose ps

Open daarna:

http://localhost:8080

Of vanaf een andere machine in het netwerk:

http://<server-ip>:8080

Stoppen:

docker compose down
Dockerfile

De site gebruikt een eenvoudige Nginx-container:

FROM nginx:alpine
COPY . /usr/share/nginx/html
EXPOSE 80

Omdat de bestanden tijdens de build naar de container worden gekopieerd, moet je na HTML/CSS/JS/media-wijzigingen opnieuw builden:

docker compose up -d --build
Nieuwe afbeeldingen toevoegen

Plaats nieuwe afbeeldingen bij voorkeur in:

assets/images/

Gebruik daarna in HTML of JavaScript bijvoorbeeld:

<img src="assets/images/voorbeeld.png" alt="Voorbeeld">

Of in JavaScript:

const IMAGE = "assets/images/voorbeeld.png";
Nieuwe geluiden toevoegen

Plaats nieuwe mp3-bestanden bij voorkeur in:

sounds/

Voorbeeld:

<audio src="sounds/voorbeeld.mp3"></audio>
Nieuwe video’s toevoegen

Plaats video’s bij voorkeur in:

video/

Voorbeeld:

<video controls>
  <source src="video/promo.mp4" type="video/mp4">
</video>
Git workflow

Controleer wijzigingen:

git status
git diff

Alles toevoegen:

git add -A

Commit maken:

git commit -m "Update Luiz-Air site"

Pushen:

git push

Voor grotere wijzigingen is een aparte branch handig:

git checkout -b mijn-wijziging
Handige controles

Zoek root-level afbeeldingen die nog niet in assets/images/ staan:

find . -maxdepth 1 -type f \( \
  -iname "*.jpg" -o \
  -iname "*.jpeg" -o \
  -iname "*.png" -o \
  -iname "*.webp" \
\) -printf "%f\n" | sort

Zoek root-level mp3’s:

find . -maxdepth 1 -type f -iname "*.mp3" -printf "%f\n" | sort

Zoek root-level mp4’s:

find . -maxdepth 1 -type f -iname "*.mp4" -printf "%f\n" | sort

Controleer of Git geen whitespace-problemen ziet:

git diff --check
Let op

Dit is een creatieve hobby-/demo-site. Eventuele security-schermen, pincodes, access panels of waarschuwingen in HTML/JavaScript zijn bedoeld voor spel en beleving.

Alles wat in HTML, CSS en JavaScript staat, is zichtbaar in de browser.
Voor echte beveiliging is server-side authenticatie nodig.

Licentie

Privé/hobbyproject van Stefan Voorbij.
