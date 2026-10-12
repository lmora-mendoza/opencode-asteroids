# AGENTS.md

Zero-dependency HTML5 Canvas game. No build, no bundler, no package manager, no tests, no lint, no CI.

## Structure

- `index.html` — canvas `800x600` + `<script src="game.js">`. Estilos inline, sin CSS externo.
- `game.js` — todo el juego en un solo archivo (`'use strict'`). Secciones: Input → Utils → Bullet → Asteroid → Ship → Particle → Estado → Update → Draw → Loop.
- `favicon.svg` — solo icono.

## Run

Abrir `index.html` directo en el navegador, o `npx serve .` y visitar `http://localhost:3000`. No hay comando de build ni dev server propio.

## Conventions (game.js)

- Inglés para código, español para HUD/textos (`SCORE`, `NIVEL`, `GAME OVER`).
- Espacio toroidal: todo movimiento usa `wrap(v, max)`. Dimensiones fijas `W=800`, `H=600`.
- `dt` clamped a `0.05` en el loop; respetar ese clamp al tocar física.
- Input por `e.code` (`ArrowLeft/Right/Up`, `Space`); `justPressed` + `pressed()` es one-shot (consume el evento) — usarlo para disparo/reinicio, `keys[]` para continuo.
- Estados: `playing | dead | gameover`. Reinicio solo con `Space` desde `gameover`.
- Balance en constantes: `RADII=[0,16,30,50]`, `SPEEDS=[0,85,55,32]`, `POINTS=[0,100,50,20]` (indexados por `size` 1–3); nave `ROT=3.5`, `THRUST=260`, `DRAG=0.987`; colisión nave usa `radius * 0.82`; spawn evita radio de `130px` del centro.
- Verificación: no hay tests. Comprobar abriendo el juego en el navegador y jugando (rotar, propulsar, disparar, partir asteroide grande → 2 medianos → 2 pequeños, morir → reaparecer, game over → reiniciar con Espacio). Revisar consola del navegador para errores.

## Gotcha

- `README.md` menciona power-ups y "estrella fugaz", pero `game.js` no los implementa. No asumir que existen.
