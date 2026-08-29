# Dell'Erba Voice: animazione del logo

[![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)](https://www.python.org/)
[![Manim](https://img.shields.io/badge/Manim-Community-5C2D91?style=for-the-badge&logo=python&logoColor=white)](https://www.manim.community/)

Animazione del logo della web radio scolastica Dell'Erba Voice, realizzata con la libreria Manim in Python. Il logo riprende il nome della radio e una barra di equalizzazione a 7 linee che "danza" con animazioni simmetriche e poi si compone nel testo finale.

Il render finale è `LogoRadio.mp4` (1080p @ 120 fps).

## Caratteristiche

- **Logo animato**: testo "DELL'ERBA VOICE" con effetto di scrittura e pulsazione leggera.
- **Equalizzatore animato**: 7 barre verticali con caps che oscillano in modo simmetrico, si compattano, si espandono e finiscono per dissolversi.
- **Render fluido**: 120 fps.
- **Stile brand radio**: palette calda crema (`#FFF5E1`) con rosso brand e accenti viola.

## Tecnologie

- **Python 3** — scripting e logica di generazione delle forme geometriche
- **Manim (Community Edition)** — engine matematico per animazioni vettoriali
- **FFmpeg** — pipeline di encoding video e rendering ad alto frame rate

## Uso

Per riprodurre il render, apri `LogoRadio.mp4` con un player video.

Per rigenerare l'animazione da zero:

```bash
manim render -q m LogoRadio.py LogoRadio
```

Qualità disponibili: `-q l` (480p), `-q m` (720p), `-q h` (1080p), `-q k` (2160p). L'output finisce in `media/videos/LogoRadio/`. Per esportarlo nella cartella del progetto:

```bash
cp "media/videos/LogoRadio/720p30/LogoRadio.mp4" .
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
├── LogoRadio.mp4    # Render finale (120 fps)
└── README.md
```

*Animazione creata da Lorenzo Recchia per la web radio scolastica Dell'Erba Voice.*
