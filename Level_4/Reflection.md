# Flexbox vs. Grid: Level 4 Reflection

**Which was easier to implement?**
Flexbox was easier for the pieces, and Grid was easier for the whole page. Flexbox handled the header (`margin-left: auto` pushes the user menu to the right edge), the card rows (`flex: 1 1 14rem` with `flex-wrap`) and the sidebars (`flex: 0 0 var(--left-w)` beside a `flex: 1 1 0` main). The four breakpoints were the hard part. At 900px the right sidebar only drops below because we give it `flex-basis: 100%`, and we needed `order: -1` to put the left sidebar before main. In Grid, each breakpoint was just a new `grid-template-areas` map.

**Which required less code?**
Grid needed less code for page structure. The card reflow was one line in both versions, `repeat(auto-fit, minmax(min(100%, 14rem), 1fr))` in Grid and `flex: 1 1 14rem` in Flexbox. The collapsible sidebars cost the same in both: JavaScript toggles a class, and CSS swaps `--left-w` for `--rail`.

**Which was more intuitive?**
Grid was more intuitive to read, because the area names look like the wireframe. Subgrid was the clearest win: the three footer link columns line up with the left sidebar, main and right sidebar above them. In Flexbox that would mean repeating the same widths in two containers. Grid also let the logo and user menu share one cell (overlapping areas) and sit at opposite ends with `justify-self`.

**When would we prefer one over the other?**
We would use Grid for the page structure and anything that must line up across containers. We would use Flexbox for one-dimensional rows, like the header, navigation and card rows, where content decides the sizes. Custom properties, `clamp()` and container queries worked the same in both. Subgrid is newer, so we wrapped it in `@supports` and the footer falls back to equal columns.

**One thing to watch**
Both versions use the same HTML, with the main content before the sidebars. That keeps the important content first for keyboard and screen-reader users, and the CSS moves the left sidebar into position on larger screens.