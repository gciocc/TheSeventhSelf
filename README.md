# The Seventh Self

**The Seventh Self** e' un'esperienza web interattiva che esplora il mito dei "sette sosia" come connessione emotiva e percettiva, non come semplice somiglianza fisica. L'utente attraversa un globo 3D, risponde a un breve profilo, scansiona o carica un volto e riceve 7 risonanze: identita' simbolicamente affini, poi sintetizzate nella figura finale dell'**Eighth Self**.

## Concept e tecnologie

Il progetto funziona come un osservatorio di identita' invisibili: usa dati visivi, domande personali, geolocalizzazione evocativa e una messa in scena 3D per costruire una costellazione narrativa attorno all'utente.

Tecnologie principali:

- **Vite** per sviluppo e build frontend.
- **JavaScript ES modules** senza framework UI.
- **Three.js** e `OrbitControls` per globo, stelle, marker, linee e interazioni 3D.
- **@vladmandic/face-api** per rilevare il volto in webcam lato client.
- **HTML/CSS custom** per layout, transizioni, profilo, scanner e overlay finale.
- **Dati statici JSON/BIN/WebP/PNG** per costellazione, embedding, atlante dei volti, texture e asset visivi.

## Architettura tecnica

La cartella sorgente principale e' `web/src/`; la build pubblicabile contiene gli stessi asset in forma statica dentro `TheSeventhSelf/`.

- `main.js`: regia dell'esperienza. Gestisce stati UI, intro, caricamento, profilo, scanner, passaggio alle 7 risonanze e comparsa dell'Eighth Self.
- `globe.js`: mondo iniziale in Three.js. Crea globo, atmosfera, campo stellare, marker dei volti, picking con raycaster e animazioni di ingresso.
- `resonanceWorld.js`: seconda scena 3D dopo la scansione. Mostra utente e 7 risonanze sul globo, collegandole con linee e animazioni di convergenza.
- `scanner.js`: acquisizione da webcam o upload. Precarica Face API, controlla permessi camera e genera il risultato in modalita' statica.
- `matcher.js`: utility per matching vettoriale su embedding a 512 dimensioni; nel flusso attuale il progetto usa una simulazione locale per restare deployabile senza backend.
- `faceAtlas.js`, `faces.js`, `facePortraitEffect.js`: caricamento dei volti da `/faces` o dagli atlas WebP, billboard 3D e shader/effetto pixel portrait.
- `geoLocations.js`, `landPoints.js`: conversione lat/lon in coordinate 3D e fallback su punti di terra emersa.
- `experienceLoader.js`, `ambientSound.js`, `narrative.js`, `resonanceCopy.js`: preload, audio ambientale e testi narrativi.
- `userProfile.js`: domande, validazione e sintesi del profilo utente.
- `eighthSelf.js`: overlay finale, scelta della risonanza conclusiva e reveal del volto.

Dati principali:

- `web/public/data/constellation.json`: 2.000 nodi usati nella costellazione, derivati da un dataset indicato come 69.987 volti.
- `web/public/data/embeddings.bin` e `embeddings_index.json`: matrice di embedding per matching vettoriale.
- `web/public/data/atlas/`: sprite atlas WebP dei volti, con manifest.
- `web/public/textures/`: texture del globo e maschera terre.

Nota: nella versione statica GitHub Pages non c'e' backend Python. Le 7 risonanze vengono scelte localmente dai dati della costellazione; la webcam serve per costruire l'esperienza e verificare la presenza del volto, non per un riconoscimento biometrico reale.

## Immagini, video e GIF

Asset visivi inclusi nel progetto:

- Logo: `assets/seventh-self-logo.png`
- Preview globo: `assets/globe-inspo-0.png`, `assets/globe-inspo-62.png`, `assets/globe-inspo-187.png`
- Preview ingresso: `assets/entry-inspo-15.png`, `assets/entry-inspo-45.png`, `assets/entry-inspo-75.png`
- Audio ambiente: `assets/ambient-space.mp3`

Per una demo video/GIF, il percorso consigliato e': intro -> esplorazione globo -> profilo -> webcam/upload -> 7 risonanze -> Eighth Self.

## Come provare l'esperienza

Online: https://gciocc.github.io/TheSeventhSelf/

In locale, dal sorgente:

```bash
npm install --prefix web
npm run dev
```

Poi aprire `http://localhost:5173`. La webcam funziona solo in contesto sicuro: `localhost` oppure HTTPS.

Build di produzione:

```bash
npm run dist
```

L'output viene generato in `web/dist/` e puo' essere pubblicato come sito statico.

## Contatti

Progetto e autorialita': **Giorgia Ciocca**  
Email: `g.ciocca@ied.edu`  
GitHub: `@gciocc`
