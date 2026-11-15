# DEALT-a-E — Color Difference Solitaire

A standalone browser game prototype based on the supplied DEALT-a-E wireframes. It includes four levels, solitaire-style stock/current-card interaction with click-to-place and drag-and-drop, a six-round mystery-hex loop, scoring, selectable ΔE76 / CIEDE2000 formulas, approximate vision simulation modes, and a research comparison panel.

## Run it

1. Download and unzip the folder.
2. Open `index.html` in a modern browser. No build step or server is required.
3. Choose one of the four levels.

For a local server (optional), open a terminal in this folder and run `python -m http.server 8000`, then visit `http://localhost:8000`.

## Notes

- ΔE76 and CIEDE2000 are both implemented from the browser-side sRGB → CIELAB conversion; screen/display differences affect the colors people see.
- The protanopia, deuteranopia, and tritanopia views are approximate matrix simulations, not clinical tools or exact representations of individual vision.
- Research comparison is exploratory. The game does not automatically upload data. The current run summary is shown at completion.
- Scoring: +100 per cleared round; +25 for no failed validations in that round; +25 for no reshuffle in that round; −10 per reshuffle; −5 per failed validation; +150 for correct final color.
- Level 4 preserves the wireframe's ΔE ≤ 35 adjacency rule. Because this is a prototype, generated puzzles can occasionally be unusually difficult; use Reset placements or reshuffle as needed.
- The project is self-contained apart from the optional Google Fonts import. If offline, it falls back to system fonts.


## Vision challenge bonus and selection clarity
- Selected cards receive a prominent purple highlight.
- Placed cards retain their hexadecimal color code in the slot.
- Open the eye icon to learn about each approximate viewing simulation.
- Selecting any non-normal simulation awards +25 points for each successfully completed round while that mode is selected.

## Stock and current card
- Draw one card at a time from the stock into the Current Card area, like a solitaire waste pile. Only the most recently drawn card is shown; the separate Drawn Cards tray is removed.
- Click a puzzle slot or drag the current card into a slot to place it. Its hex code remains visible after placement.
- When the stock is empty, the stock area shows a refresh symbol. Refreshing shuffles unplaced drawn cards back into the stock and applies the reshuffle penalty. Cards already placed in puzzle slots are not recycled.


## Matching and mystery hex update
- In Levels 1 and 2, validate only after the stock has been drawn through so the choice can be checked against all candidate cards seen in the round. The correct match is the lowest ΔE under the currently selected formula, not the first card dealt.
- The final mystery challenge shows the six-digit hex code and four color options without displaying the answer swatch first.
- A first-time tutorial explains RR (red), GG (green), and BB (blue) with arrows. The Color Science & Code Guide now explains hexadecimal/base-16 digits and RGB channel values in more detail.


### Matching logic update

For Levels 1 and 2, the game evaluates every candidate in the round before it is drawn, including cards still in the stock. Players do not need to exhaust the deck to validate a correct lowest-ΔE match. Level 1 accepts the placed card only if it has the lowest ΔE against the target among all round candidates; Level 2 checks each placed card against all candidates for its target. If a closer card remains in the stock, validation explains that another card is closer and lets the player keep drawing.

## Level 2 partial-match locking

Level 2 now lets players validate their current pairings without having to fill every target first. Each correct target match is locked in place and marked with a green locked indicator. The player can replace only incorrect pairings, and validation feedback shows the selected card's ΔE, the lowest available ΔE for that target, and the difference between them. Locked matches remain in place when the player resets the other placements. The round advances when all three target matches are correct and locked.
