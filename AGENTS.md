# Soc Ops — Agent Instructions

Social Bingo game for in-person team mixers. Spring Boot 3.4.2 + Thymeleaf + Java 21, no database.

## Commands

```bash
cd socops
./mvnw spring-boot:run          # dev server at http://localhost:8080 (DevTools live-reload)
./mvnw clean package            # build
./mvnw test                     # unit tests
```

## Architecture

```
BingoRestController   → serves GET / (Thymeleaf) + GET /api/bingo/fresh-board (JSON)
BoardAssembler        → pure-static game logic: board creation, cell flip, win detection
IcebreakerPrompts     → prompt bank (exactly 24 strings — one per non-free tile)
BingoCell             → Java record (id, prompt, selected, freeCell)
WinningStreak         → Java record (direction, index, cellPositions)
PlayPhase             → enum LOBBY | ACTIVE | VICTORY
```

**Board invariants:** 5×5 grid (25 cells), center slot 12 is always the free space (pre-selected), 24 prompts drawn from `IcebreakerPrompts.ALL_PROMPTS`. Shuffled on each `fresh-board` call. No server-side session state — the board lives in the browser.

## Frontend

- Single Thymeleaf template: [`socops/src/main/resources/templates/game.html`](socops/src/main/resources/templates/game.html)
- Styling: custom Tailwind-like utility classes in [`socops/src/main/resources/static/css/app.css`](socops/src/main/resources/static/css/app.css) — see [`.github/instructions/css-utilities.instructions.md`](.github/instructions/css-utilities.instructions.md) for the full class catalogue
- Vanilla JS only (no build step, no npm). JS lives inline at the bottom of `game.html`.
- For new UI components follow [`.github/instructions/frontend-design.instructions.md`](.github/instructions/frontend-design.instructions.md)

## Conventions

- Models are Java **records** — keep them immutable
- `BoardAssembler` is a **final class with only static methods** — no Spring injection
- Tests live in `BoardAssemblerTests.java` and use JUnit 5 with `@DisplayName` for readability
- `IcebreakerPrompts.ALL_PROMPTS` must stay at exactly **24 entries**; adding more requires also removing some

## Custom Agents (`.github/agents/`)

| Agent | Purpose |
|-------|---------|
| `quiz-master` | Generate themed icebreaker prompts |
| `tdd` | Orchestrate full Red→Green→Refactor TDD cycle |
| `tdd-red` / `tdd-green` / `tdd-refactor` | Individual TDD phases |
| `ui-review` | Review and critique the frontend UI |
| `pixel-jam` | Visual/creative frontend work |

## Lab Workshop

Step-by-step exercises are in [`workshop/`](workshop/00-overview.md). Follow them in order (00 → 04).
