# Signals from Mars

An interactive web experience where visitors tune in to the "silent signals" of eight NASA robots on Mars and hear their stories told in the first person. A prototype for the **NASA Space Apps Challenge 2026**. This is not an official NASA product.

**Robots:** Viking 1, Viking 2, Sojourner, Spirit, Opportunity, Phoenix, InSight, and Ingenuity.

## Features

- **Tuning console:** A radio dial, a 3D globe, and a flat map of Mars, with each robot placed at its real latitude and longitude. Tuning in to a signal adds it to the progress counter (0/8).
- **Four story chapters per robot:** Arrival, My Body, What I Discovered, and My Last Day. Each chapter can be read or listened to, with word-by-word highlighting during narration.
- **One mini-activity per robot:**

  | Robot | Activity |
  |---|---|
  | Viking 1 | `foto` |
  | Viking 2 | `escarcha` |
  | Sojourner | `manejar` |
  | Spirit | `rueda` |
  | Opportunity | `odometro` |
  | Phoenix | `hielo` |
  | InSight | `sismo` (featuring the real recording of a marsquake from sol 173) |
  | Ingenuity | `vuelo` |

- **Real NASA photographs and 3D models** (four of the models come from NASA; the Phoenix and Sojourner models were created by the team).
- **Mission lifeline** (how long each robot operated compared with its expected lifetime) and **mission relay timeline** (how each mission paved the way for the next).
- **Mars Guardian card:** After tuning in to all eight robots, visitors can sign the card with their name and download it as a PNG.
- **"Is It True?" section:** Sources, debunked myths, and facts for which sources disagree.
- **Bilingual interface** (Spanish / English), light and dark themes, and support for `prefers-reduced-motion`.

## How to run

No build step or dependencies to install. Open `Signals_from_Mars.html` in a modern web browser **with an internet connection**.

If the 3D globe or models do not load when opening the file locally, serve it through any static web server:

```bash
python3 -m http.server 8000
# Then open http://localhost:8000/Signals_from_Mars.html
```

To jump directly to a robot, use its URL hash: `#viking1`, `#viking2`, `#sojourner`, `#spirit`, `#opportunity`, `#phoenix`, `#insight`, or `#ingenuity`.

## External resources (loaded over the internet)

| Resource | Source |
|---|---|
| three.js 0.160.0 + Draco decoder | cdn.jsdelivr.net |
| Inter and DM Mono fonts | Google Fonts |
| 3D models (`.glb`) | `nasa/NASA-3D-Resources` on GitHub and assets.science.nasa.gov |
| Marsquake recording (InSight) | NASA's SoundCloud player |

NASA photographs and the Mars texture are **embedded as base64 data** in the HTML, which is why the file is approximately 1.7 MB.

## Code structure

Everything is contained in a single `.html` file (CSS, HTML, and JavaScript). The main parts of the script are:

- `R`: Data for each robot (coordinates, dates, text in `es` and `en`, the four chapters in `ch`, and the activity specified by `game`).
- `TABS`: The four story chapters.
- `GAMES`: The mini-activities, with one function per robot.
- `IMG` and `MEDIA`: Embedded photographs, captions, and credits.
- `NASA3D`: 3D models and their animatable parts.
- `VOICES` / `VPROF`: Voice tone and speed settings for each robot (using the browser's speech synthesis).
- `SRC`: List of sources displayed on the page.
- `sfx`: Sounds generated with Web Audio.

## Data stored in the browser

The site uses `localStorage` with these keys: `sdm2-lang` (language), `sdm2-sound` (sound), `sdm2-voice` (automatic narration), `sdm2-heard` (recovered signals), and `sdm2-name` (name on the card). The "Start Over" button clears the saved progress.

## Credits and sources

Mission data comes from [NSSDCA](https://nssdc.gsfc.nasa.gov/) and [NASA Science](https://science.nasa.gov/). NASA photographs, the Mars map, and 3D models (public-domain material) come from the [NASA Image and Video Library](https://images.nasa.gov/) and [NASA 3D Resources](https://github.com/nasa/NASA-3D-Resources). InSight marsquake recordings: NASA/JPL-Caltech, Charalambous, and Fuji (IPGP).

## Known limitations

- An internet connection is required for 3D assets, fonts, and SoundCloud.
- Narration uses voices available in the browser, so voices vary by operating system.
- InSight's real audio recording depends on the SoundCloud player and the browser's autoplay restrictions.
