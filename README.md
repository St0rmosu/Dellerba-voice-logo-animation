# Dell'Erba Voice — Animazione del logo

[![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)](https://www.python.org/)
[![Manim](https://img.shields.io/badge/Manim-Community-5C2D91?style=for-the-badge&logo=python&logoColor=white)](https://www.manim.community/)

Animazione del logo della web radio scolastica **"Dell'Erba Voice"**, realizzata con la libreria **Manim** in Python. Il logo riprende il nome della radio e una barra di equalizzazione a 7 linee che "danza" con animazioni simmetriche e poi si compone nel testo finale.

## Caratteristiche

- **Logo animato**: testo "DELL'ERBA VOICE" con effetto di scrittura e leggero pulsare.
- **Equalizzatore animato**: 7 barre verticali con caps che oscillano in modo simmetrico, si compattano, si espandono e infine si dissolvono.
- **Render ad alta fluidità**: frame rate 120 fps per un movimento estremamente smooth.
- **Stile brand radio**: palette calda crema (`#FFF5E1`) con rosso brand e accenti viola.

## Tech Stack

- **Python 3** — Scripting e logica di generazione delle forme geometriche
- **Manim (Community Edition)** — Engine matematico per animazioni vettoriali fluide
- **FFmpeg** — Pipeline di encoding video e rendering ad alto frame-rate

## Architettura

Una singola scena `LogoRadio` che orchestra tutte le animazioni in sequenza:

```
                 ┌─────────────────────────────┐
                 │   Scene: LogoRadio (Scene)  │
                 ├─────────────────────────────┤
                 │  1. Equalizzatore (7 barre) │
                 │     · wave simmetrica       │
                 │     · compattazione         │
                 │     · espansione            │
                 │  2. Write "DELL'ERBA VOICE" │
                 │  3. Pulsazione del titolo   │
                 │  4. Fade out finale         │
                 └──────────────┬──────────────┘
                                ▼
                      Manim → FFmpeg
                         LogoRadio.mp4
```

Gli elementi base sono `Line` (barre), `Dot` (caps) e `Text`; l'animazione simmetrica superiore/inferiore è ottenuta con `put_start_and_end_on` e `there_and_back` come rate function.

## Project Structure

```
Dellerba-voice-logo-animation/
├── LogoRadio.py     # Scena Manim (definizione completa dell'animazione)
├── LogoRadio.mp4    # Render finale (120 fps)
└── README.md
```

## Installation & Setup

Prerequisiti: Python 3.9+, [Manim Community Edition](https://docs.manim.community/) e FFmpeg.

```bash
# su Arch (yay) / altri sistemi: installa manim e ffmpeg
yay -S manim ffmpeg            # Arch/Manjaro
pip install manim              # alternativa via pip

git clone https://github.com/St0rmosu/Dellerba-voice-logo-animation.git
cd Dellerba-voice-logo-animation
```

Per riprodurre il render: apri `LogoRadio.mp4` con qualsiasi player video.

## Usage

Per rigenerare l'animazione da zero:

```bash
manim render -q m LogoRadio.py LogoRadio
```

Le qualità disponibili: `-q l` (480p), `-q m` (720p), `-q h` (1080p), `-q k` (2160p). L'output viene scritto in `media/videos/LogoRadio/`; per esportarlo nella cartella del progetto:

```bash
cp "media/videos/LogoRadio/720p30/LogoRadio.mp4" .
```

> Nota: la scena imposta `self.renderer.camera.frame_rate = 120`, quindi verifica che il file generato usi i 120 fps.

## Screenshots / Demo

<video src="LogoRadio.mp4" controls width="640"></video>

## API Documentation

Nessuna API esterna: il progetto è un puro script di rendering offline. Le uniche "interfacce" sono il CLI di Manim (`manim render ...`) e la classe `LogoRadio` come punto di estensione per nuove varianti del logo.

## Engineering Decisions

- **120 fps**: scelta per un'animazione ultra-smooth, particolarmente importante per l'equalizzatore; il costo è un render più lungo e un file più pesante.
- **Animazione simmetrica via rate function**: `there_and_back` garantisce che caps e barre si muovano specularmente sopra/sotto lo zero, mantenendo il design coerente.
- **Coordinate parametriche**: altezze, posizioni e spessori delle barre sono definiti in liste, per ritoccare il design senza riscrivere le animazioni.

## Limitations & Future Improvements

- Font "Aerospace Bold" richiesto dal codice: se assente, Manim usa un fallback e il testo potrebbe apparire diverso.
- Durata e struttura fisse della scena: le varianti del logo richiedono modifica del codice.
- Prossimi passi: parametrizzare colori/tempi tramite configurazione, aggiungere varianti (logo statico, versione invertita), supportare testo alternativo per altre radio, ottimizzare con low-level Manim (`VectorizedVMobject`) per render più rapidi.

---

*Animazione creata da Lorenzo Recchia per la web radio scolastica "Dell'Erba Voice".*
