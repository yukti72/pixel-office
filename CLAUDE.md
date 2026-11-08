# Pixel Office

A single-page pixel-art office scene: four characters work at desks, then walk around (coffee, snacks, sofa, meeting room, lounge). Milo the dog wanders and plays. Clicking a person opens their "character file" card.

## Run it
Static site, no build step. Open `index.html` in a browser, or run `python3 -m http.server` in this folder and open http://localhost:8000. It needs internet only for Google Fonts.

## Layout
- `index.html` holds everything: styles, the markup for the character-file modal, and one `<script>`.
- `assets/` holds all images:
  - `office.png` is the map (1671x941). Chairs are NOT baked in; they are drawn from `chair_full.png`.
  - `<name>_walk.png`, `<name>_idle.png` are 6-frame horizontal strips; `<name>_sit.png` is the seated pose. Names: curly, short, long, wavy.
  - `milo_walk.png`, `milo_idle.png` are Milo's strips.
- `docs/pixel-wars-mockup.png` is the reference mockup for the planned Pixel Wars mini-game.

## Code map (inside index.html)
- `CONFIG` at the top: characters (name, sprite sheets, seat index, `profile` for the character file), seat x positions, desk and chair y values, and `places` (coffee, sofa, shelf, lounge, meeting, snack) with stand-spots. Edit here to add people or move things.
- Walkable grid: `ADD` (walkable rectangles) and `OBS` (furniture blockers), A* pathfinding in `findPath`.
- `class Person` (state machine: seated, standing, walking, idle, sitting, sofaUp), `class Dog`.
- Click handling: `hitAt`, then `openFile(person)` for the character card.
- Test hooks I used: `people`, `dog`, `paused`, `render()` are globals, so a headless browser can step the simulation.

## Rules for changes
- Do not redesign or replace the map, characters, furniture or sprite sheets unless asked.
- Seated people are clipped at the desk edge (`seatClipY`); the chair rolls out when they stand.
- Keep pixel rendering crisp (no smoothing on sprites).

## Planned: Pixel Wars
Multiplayer drawing contest: 32x32 canvas, 8 fixed colours, pen/eraser/undo/redo, 60 s per round, 3 rounds, vote for others (20 s), one point per vote. Launch from the meeting-room TV. Needs a realtime backend (not present yet). Plan first, get approval, then build the editor first and test each phase.
