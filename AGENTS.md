# Soc Ops — Agent Instructions

Social Bingo for in-person team mixers. Spring Boot 3.4.2 + Thymeleaf + Java 21, no database.

## Mandatory Dev Checklist

Before marking any task complete, run all three from `socops/`:

```bash
./mvnw clean package -q   # build — must succeed with no errors
./mvnw test               # tests — all must pass
# no dedicated lint step; compiler warnings are treated as errors
```

## Commands

```bash
cd socops
./mvnw spring-boot:run    # dev server → http://localhost:8080 (DevTools live-reload)
```

## Architecture

```
BingoRestController  → GET / (Thymeleaf) + GET /api/bingo/fresh-board (JSON)
BoardAssembler       → static-only: board creation, cell flip, win detection
IcebreakerPrompts    → prompt bank — exactly 24 entries (one per non-free tile)
BingoCell / WinningStreak / PlayPhase  → immutable Java records / enum
```

Board: 5×5 grid, center slot 12 = free space, state lives in the browser only.

## Frontend

- Template: [game.html](socops/src/main/resources/templates/game.html) — vanilla JS inline at the bottom
- CSS utilities: [app.css](socops/src/main/resources/static/css/app.css) — see [css-utilities.instructions.md](.github/instructions/css-utilities.instructions.md)
- New UI work: follow [frontend-design.instructions.md](.github/instructions/frontend-design.instructions.md)

## Conventions

- Models are Java **records** — immutable, no setters
- `BoardAssembler` is `final` with only `static` methods — never inject via Spring
- `IcebreakerPrompts.ALL_PROMPTS` must stay at exactly **24 entries**
- Tests use JUnit 5 + `@DisplayName` in `BoardAssemblerTests.java`

## Agents (`.github/agents/`)

`quiz-master` · `tdd` · `tdd-red` · `tdd-green` · `tdd-refactor` · `ui-review` · `pixel-jam`

Workshop exercises: [`workshop/`](workshop/00-overview.md) — follow in order 00 → 04.
