# Flexbox vs. Grid: Level 2 Reflection

**Which was easier to implement?**
For this layout, Flexbox was slightly easier. A main area with one sidebar is a single row that wraps, so we needed two containers (`.layout` as a column and `.columns` as a wrapping row) and a `flex-basis` of 70% and 30%. The mobile layout came almost for free: giving both children `flex: 1 1 100%` makes each take a full row. Grid needed us to plan the area names first, but after that the desktop and mobile layouts were just two different maps.

**Which required less code?**
Flexbox did, by a small margin: about five layout rules against about eight for Grid, because Grid needs a `grid-area` line for every region plus two `grid-template-areas` maps. Grid's code was longer but more explicit. `7fr 3fr` states the split directly, while `flex-basis: 70%` and `30%` only work because they add up to 100% and nothing else takes space. Grid also cost us one workaround: the `.columns` wrapper exists for the flexbox version, so the Grid file sets it to `display: contents`.

**Which was more intuitive?**
Grid was more intuitive to read. The string `"main sidebar"` looks like the wireframe in the brief, so the layout is visible in the code. Flexbox was less obvious: nothing in the flexbox CSS says "stack on mobile". Stacking happens only because each item has a 100% basis and the container is allowed to wrap. That worked, but we had to understand wrapping before we could trust it.

**When would we prefer one over the other?**
We would use Flexbox for one-dimensional groups where the content decides the sizes, like the navigation menu or a row of buttons. We would use Grid for the page structure, where regions should line up in rows and columns and we want to rearrange them by editing a map. For a two-region page like this one either works. As a page grows, for example with a second sidebar, Grid scales better because we edit the map instead of adding more basis and order rules.