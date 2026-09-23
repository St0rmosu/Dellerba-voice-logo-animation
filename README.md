# Dell'Erba Voice: animazione del logo

[![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)](https://www.python.org/)
[![Manim](https://img.shields.io/badge/Manim-Community-5C2D91?style=for-the-badge&logo=python&logoColor=white)](https://www.manim.community/)

Animazione del logo della web radio scolastica Dell'Erba Voice, realizzata con la libreria Manim in Python. Il logo riprende il nome della radio e una barra di equalizzazione a 7 linee che "danza" con animazioni simmetriche e poi si compone nel testo finale.

Il render finale è `LogoRadio.mp4` (2160p @ 60 fps).

## Caratteristiche

- **Logo animato**: testo "DELL'ERBA VOICE" con effetto di scrittura e leggero pulsare.
- **Equalizzatore animato**: 7 barre verticali con caps che oscillano in modo simmetrico, si compattano, si espandono e infine si dissolvono.
- **Render ad alta risoluzione**: 2160p @ 60 fps, con frame rate della scena impostato a 120.
- **Stile brand radio**: palette calda crema (`#FFF5E1`) con rosso brand e accenti viola.

## Tecnologie

- **Python 3** — scripting e logica di generazione delle forme geometriche
- **Manim (Community Edition)** — engine matematico per animazioni vettoriali
- **FFmpeg** — pipeline di encoding video e rendering ad alto frame rate

## Uso

Per riprodurre il render, apri `LogoRadio.mp4` con un player video.

Per rigenerare l'animazione da zero:

```bash
manim render -q k LogoRadio.py LogoRadio
```

Qualità disponibili: `-q l` (480p), `-q m` (720p), `-q h` (1080p), `-q k` (2160p). L'output finisce in `media/videos/LogoRadio/`. Per esportarlo nella cartella del progetto:

```bash
cp "media/videos/LogoRadio/2160p60/LogoRadio.mp4" .
```

## Architettura

Una singola scena `LogoRadio` orchestra tutte le animazioni in sequenza:

![Diagramma architettura](docs/architecture.png)

Gli elementi base sono `Line` (barre), `Dot` (caps) e `Text`. L'animazione simmetrica sopra e sotto lo zero usa `put_start_and_end_on` con `there_and_back` come rate function.

## Installazione

Prerequisiti: Python 3.9+, [Manim Community Edition](https://docs.manim.community/) e FFmpeg.

```bash
yay -S manim ffmpeg            # Arch/Manjaro
pip install manim              # alternativa via pip

git clone https://github.com/St0rmosu/Dellerba-voice-logo-animation.git
cd Dellerba-voice-logo-animation
```

## Struttura del progetto

```
Dellerba-voice-logo-animation/
├── LogoRadio.py     # Scena Manim (definizione completa dell'animazione)
├── LogoRadio.mp4    # Render finale (2160p @ 60 fps)
└── README.md
```

## Engineering Decisions

- **Fps**: la scena imposta `frame_rate = 120`; il preset di qualità di Manim (`-q k` = 2160p60, `-q h` = 1080p60) determina il frame rate effettivo dell'output (60 fps). Fps più alti costano render più lunghi e file più pesanti.
- **Animazione simmetrica via rate function**: `there_and_back` garantisce che caps e barre si muovano specularmente sopra/sotto lo zero, mantenendo il design coerente.
- **Coordinate parametriche**: altezze, posizioni e spessori delle barre sono definiti in liste, per ritoccare il design senza riscrivere le animazioni.

## Limitations & Future Improvements

- Font "Aerospace Bold" richiesto dal codice: se assente, Manim usa un fallback e il testo potrebbe apparire diverso.
- Durata e struttura fisse della scena: le varianti del logo richiedono modifica del codice.
- Prossimi passi: parametrizzare colori/tempi tramite configurazione, aggiungere varianti (logo statico, versione invertita), supportare testo alternativo per altre radio, ottimizzare con low-level Manim (`VectorizedVMobject`) per render più rapidi.

---

*Animazione creata da Lorenzo Recchia per la web radio scolastica "Dell'Erba Voice".*
