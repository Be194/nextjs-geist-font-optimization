Below is the detailed plan for implementing “GUARDIÃO DO REINO” as a single-page HTML game. This plan explains every major section—from the HTML structure and CSS styling to the JavaScript classes, game loop, input handling, audio integration, and responsiveness. Since all code will reside in one file (for example, guardiao_reino.html), no external modules or libraries are needed.

---

**1. File Creation and Overall Structure**  
- Create a new file named “guardiao_reino.html” (this file is self-contained).  
- Ensure the file includes a full HTML document structure with a proper DOCTYPE, <html>, <head>, and <body> sections.  
- Confirm that all dependent sections (CSS styling, JavaScript code, and HTML UI elements) are defined within this file.

---

**2. HTML Structure**  
- In the <head> tag:  
  – Add a <meta> viewport tag for responsiveness.  
  – Set the page <title> to “GUARDIÃO DO REINO”.  
  – Include a <style> block with all the CSS (see below).  
- In the <body> tag, include the following major sections:  
  – A header element that displays the title at the top.  
  – A HUD panel at the very top to show the castle’s life bar, a blue mana bar immediately underneath, and counters for wave, score (inimigos/pontos) and moedas.  
  – A main game area containing a <canvas> element (id="gameCanvas") which will be used to render the game scene (castle, guardian, enemies, projectiles, particle effects, etc.).  
  – A sidebar containing upgrade buttons (each button labeled per upgrade: “Aumentar dano”, “Aumentar mana máxima”, “Regeneração mais rápida”, “Vida extra para o castelo”) that will trigger the upgrade functions.  
  – An overlay <div> for feedback messages such as “Onda Completa!”, “Upgrade Comprado!”, Game Over screens, and Victory screens.

---

**3. CSS Styling (Embedded in a <style> Block)**  
- Define a fantasy medieval themed palette (e.g. deep purples, golds, dark greens) applied via background colors, borders, and typography.  
- Style the header with bold fonts and centered text.  
- Create distinct visual styles for the HUD’s life (red/green gradient) and mana (blue gradient) bars with smooth CSS transitions.  
- Style the <canvas> area ensuring it resizes (using CSS flexbox/grid and media queries) for mobile and desktop.  
- Design the upgrade sidebar and buttons with modern minimalist layouts (spacing, padding, hover transitions) without using any external icon libraries.  
- Include graceful fallbacks for any images (if later added via <img> tags) using the onerror attribute.

---

**4. JavaScript Implementation (Inside a <script> Tag at the End of the Body)**  
- Use Object-Oriented Programming with clearly defined ES6 classes:  
  – Game: Manages the overall game loop (using requestAnimationFrame), waves of enemy spawn, collision detection, HUD updates, and game state transitions (running, paused, game over, victory).  
  – Player (Guardian): Represents the magic guard, handling mana, the basic attack (mouse click for 10 damage with no mana cost), and special attacks.  
  – Enemy: Represents each enemy type (Goblins, Orcs, Lobos; and boss Dragão) with properties: health, speed (normal, slow, fast), and rewards (coins).  
  – Projectile: For animated spells (fireball and ice lightning) with properties such as position, speed, area of effect (AOE for fireball), and slow effect (for ice lightning).  
- Implement Input Controls:  
  – Attach a “click” listener on the canvas for basic attacks (calculating click coordinates versus enemy positions).  
  – Add keydown listeners:  
    - “F” triggers fireball (consumes 15 mana and deals 25 AOE damage).  
    - “R” triggers raio congelante (consumes 20 mana, deals 15 damage, and applies a slow debuff).  
    - “P” toggles pause.  
    - “SPACE” starts the next wave if the current one is over.  
  – For mobile, add touch event listeners that mimic mouse click behavior.  
- Implement Wave Handling:  
  – Wave 1–3: Spawn only goblins.  
  – Wave 4–6: Spawn goblins and orcs.  
  – Wave 7–9: Spawn a mixed group (goblins, orcs, lobos).  
  – Wave 10: Spawn the boss (Dragão) together with minion enemies.  
  – When a wave is cleared, display a “Onda Completa!” message in the overlay and wait for SPACE to progress.  
- Build the Upgrade Shop:  
  – Create upgrade functions that are invoked on sidebar button clicks.  
  – Check if the player has enough moedas (coins) before applying upgrades:  
    - Aumentar dano: +5 dano (cost: 50 moedas)  
    - Aumentar mana máxima: +10 mana (cost: 40 moedas)  
    - Regeneração mais rápida: (cost: 60 moedas)  
    - Vida extra: +25 à vida do castelo (cost: 80 moedas)  
  – On a successful purchase, deduct coins, update HUD stats, and show “Upgrade Comprado!” feedback.  
- Integrate Audio using the Web Audio API:  
  – Initialize an AudioContext (with proper try-catch for error handling).  
  – Load or generate sound effects for:  
    - Background musical loop (épica medieval),  
    - Magic casting (raio and fireball whoosh and explosion sounds),  
    - Enemy grunhidos, and  
    - Feedback for upgrades and game events (explosions, game over).  
- Ensure Error Handling and Best Practices:  
  – Check if the browser supports canvas and AudioContext.  
  – Use try-catch where appropriate (especially in audio initialization and game loop functions).  
  – Use clear inline comments to explain each section, declare variables with const/let, and use template literals when needed.

---

**5. Responsiveness and UI/UX Considerations**  
- Use CSS media queries to adjust layout and font sizes on mobile devices.  
- For touch devices, ensure the canvas receives touchstart events along with responsive upgrade button sizes.  
- Maintain clear visual hierarchy: prominent HUD information, intuitive upgrade menus, and smooth transitions (both visual and audio) for game events.  
- Optimize the game loop performance via requestAnimationFrame; include collision efficiency measures and smooth projectile animations.  
- Provide visual feedback (e.g., screen shake effect when the castle é atingido) and particle effects (magical explosions) to enrich the experience.

---

**6. Testing and Debugging**  
- Verify that the canvas initializes and renders correctly on both desktop and mobile.  
- Test each attack (click, F, R), ensuring proper mana consumption and enemy damage.  
- Simulate enemy collisions with the castle, upgrade purchases, and validate that the HUD updates accurately.  
- Confirm that audio plays smoothly and does not break the game loop.  
- Ensure the game state (paused, game over, victory) triggers the appropriate overlays and restart options.

---

**Summary**  
- A new “guardiao_reino.html” file will encapsulate all HTML, CSS, and JavaScript code.  
- The HTML structure includes a header, HUD with life/mana/wave/score, a canvas for the game’s visuals, an upgrade sidebar, and an overlay for feedback messages.  
- CSS creates a modern, fantasy medieval theme with responsive design and smooth transitions.  
- JavaScript uses ES6 classes (Game, Player, Enemy, Projectile) to drive the gameplay, input handling, wave progression, and upgrades while ensuring robust error handling.  
- Controls include mouse clicks for basic attacks and key events (“F”, “R”, “P”, “SPACE”) for special skills, with touch support for mobile.  
- Audio is integrated using the Web Audio API with fallback error handling.  
- The game loop is optimized via requestAnimationFrame with built-in collision detection and state management.  
- All features are designed with clear UI/UX principles for an immersive castle-defense experience.
