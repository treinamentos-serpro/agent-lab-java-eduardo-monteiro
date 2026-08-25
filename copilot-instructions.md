# Copilot instructions

## Design guide

This project uses a lightweight, utility-first CSS approach for the Spring Boot + Thymeleaf UI. Keep new UI work aligned with the existing styling system and the visual language already established in the app.

### Core principles

- Prefer reusable utility classes over custom ad hoc CSS when possible.
- Build on the utility patterns already defined in [socops/src/main/resources/static/css/app.css](socops/src/main/resources/static/css/app.css).
- Match the game UI structure and conventions in [socops/src/main/resources/templates/game.html](socops/src/main/resources/templates/game.html).
- Keep layouts simple, readable, and focused on the game experience; avoid adding unnecessary visual noise.

### Visual direction

- Favor distinctive, polished styling rather than generic "AI default" designs.
- Use a coherent palette with sharp accents and strong contrast.
- Prefer thoughtful typography, spacing, and rhythm over heavy ornamentation.
- Use gradients, soft depth, and subtle motion carefully to create atmosphere without overwhelming the interface.
- Stick to CSS variables and composable utility classes for consistency.

### Styling constraints

- Use utility classes such as `flex`, `grid`, `gap-*`, `rounded-*`, `shadow-*`, `text-*`, `bg-*`, `border`, and `transition-*` when composing layouts.
- Keep CSS specificity low and avoid introducing large custom selectors unless necessary.
- If new styling is required, add it in the shared stylesheet instead of scattering one-off rules across templates.
- Maintain responsiveness and accessibility: readable contrast, clear focus states, and predictable interaction feedback.

### Frontend expectations

- New UI work should feel intentional and tailored to the social mixer experience.
- Keep the design playful, approachable, and friendly without becoming cluttered.
- For interactive states, use subtle transitions and lightweight motion rather than heavy animations.
- Favor clarity of information over novelty; the interface should support the game flow before it impresses visually.

### Implementation reminder

When editing the frontend, reuse current project patterns and avoid introducing unrelated design systems or libraries. The goal is to keep the app cohesive and easy to maintain while delivering a polished experience.
