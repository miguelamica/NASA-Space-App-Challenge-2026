# Señales de Marte

Experiencia web interactiva para sintonizar las "señales dormidas" de 8 robots de la NASA en Marte y escuchar su historia en primera persona. Prototipo para el **NASA Space Apps Challenge 2026**. No es un producto oficial de la NASA.

**Robots:** Viking 1, Viking 2, Sojourner, Spirit, Opportunity, Phoenix, InSight e Ingenuity.

## Qué incluye

- **Consola de sintonía:** un dial, un globo 3D y un mapa plano de Marte con cada robot en su latitud y longitud reales. Sintonizar una señal la suma al progreso (0/8).
- **Historia por robot en 4 capítulos:** Llegada, Mi cuerpo, Lo que descubrí y Mi último día. Cada uno se puede leer o escuchar en voz alta con texto resaltado palabra por palabra.
- **Una mini-actividad por robot:**

  | Robot | Actividad |
  |---|---|
  | Viking 1 | `foto` |
  | Viking 2 | `escarcha` |
  | Sojourner | `manejar` |
  | Spirit | `rueda` |
  | Opportunity | `odometro` |
  | Phoenix | `hielo` |
  | InSight | `sismo` (con la grabación real del marsquake del sol 173) |
  | Ingenuity | `vuelo` |

- **Fotos y modelos 3D reales de la NASA** (cuatro de los modelos son de la NASA; los de Phoenix y Sojourner son propios).
- **Línea de vida** (cuánto duró cada robot vs. lo esperado) y **línea de relevos** (qué le dejó cada robot al siguiente).
- **Tarjeta de Guardián:** al sintonizar los 8 robots se puede firmar con un nombre y descargar la tarjeta como PNG.
- **Sección "¿Es verdad?":** fuentes, mitos descartados y datos en los que las fuentes no coinciden.
- **Bilingüe** (español / English), tema claro y oscuro, y respeto de `prefers-reduced-motion`.

## Cómo usarlo

No hay build ni dependencias que instalar. Abrí `señales-de-marte.html` en un navegador moderno **con conexión a internet**.

Si el 3D o los modelos no cargan al abrirlo como archivo local, servilo con cualquier servidor estático:

```bash
python3 -m http.server 8000
# y abrí http://localhost:8000/señales-de-marte.html
```

Para ir directo a un robot se puede usar el hash en la URL: `#viking1`, `#viking2`, `#sojourner`, `#spirit`, `#opportunity`, `#phoenix`, `#insight`, `#ingenuity`.

## Recursos externos (se cargan por internet)

| Qué | De dónde |
|---|---|
| three.js 0.160.0 + decodificador Draco | cdn.jsdelivr.net |
| Fuentes Inter y DM Mono | Google Fonts |
| Modelos 3D (`.glb`) | `nasa/NASA-3D-Resources` en GitHub y assets.science.nasa.gov |
| Grabación del marsquake (InSight) | Reproductor de SoundCloud de la NASA |

Las fotos de la NASA y la textura de Marte van **embebidas en base64** dentro del HTML, por eso el archivo pesa cerca de 1,7 MB.

## Estructura del código

Todo está en un único `.html` (CSS, HTML y JS). Lo principal del script:

- `R`: los datos de cada robot (coordenadas, fechas, textos en `es` y `en`, los 4 capítulos en `ch`, y qué actividad usa en `game`).
- `TABS`: los 4 capítulos.
- `GAMES`: las mini-actividades, una función por robot.
- `IMG` y `MEDIA`: fotos embebidas y sus epígrafes y créditos.
- `NASA3D`: modelos 3D y sus partes animables.
- `VOICES` / `VPROF`: perfil de tono y velocidad de la voz de cada robot (síntesis de voz del navegador).
- `SRC`: lista de fuentes que se muestra en la página.
- `sfx`: sonidos generados con Web Audio.


## Datos guardados en el navegador

Usa `localStorage` con estas claves: `sdm2-lang` (idioma), `sdm2-sound` (sonido), `sdm2-voice` (voces automáticas), `sdm2-heard` (señales recuperadas) y `sdm2-name` (nombre de la tarjeta). El botón "Empezar de nuevo" de la página borra el progreso.

## Créditos y fuentes

Datos de [NSSDCA](https://nssdc.gsfc.nasa.gov/) y [NASA Science](https://science.nasa.gov/). Fotos, mapa de Marte y modelos 3D de la NASA (material de dominio público), de [NASA Image and Video Library](https://images.nasa.gov/) y [NASA 3D Resources](https://github.com/nasa/NASA-3D-Resources). Grabaciones de los marsquakes de InSight: NASA/JPL-Caltech, Charalambous y Fuji (IPGP).

## Limitaciones conocidas

- Necesita internet (3D, fuentes y SoundCloud).
- La voz usa las voces del navegador, así que cambia según el sistema operativo.
- El audio real de InSight depende del reproductor de SoundCloud y del autoplay del navegador.
