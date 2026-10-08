# Flexbox vs. Grid: Level 3 Reflection

**Which was easier to implement?**
Grid was easier for this level. With three columns and three different screen layouts, the Flexbox version needed a `flex` value and an `order` for every region at every breakpoint, and the tablet layout only works because `main` takes a 100% basis and pushes the two 50% sidebars onto a second line. In Grid we drew each layout as a map: `"left main right"` on desktop, `"main main" / "left right"` on tablet, and a single column on mobile. Moving the main content above the sidebars did not need `order` at all, because the area names decide where each region goes regardless of the HTML order.

**Which required less code?**
The Grid layout code was shorter. The Flexbox media queries repeat `flex` and `order` for `main`, `.left-sidebar` and `.right-sidebar` in both breakpoints, while the Grid media queries only change two properties on one element, `.layout`. The card row was the exception. Flexbox handled it with one rule (`flex: 1 1 200px`), and when only two cards fit, the third one stretches across the last line on its own. Grid's `repeat(auto-fit, minmax(200px, 1fr))` gives the same columns, but to make the leftover card fill its row we had to add a container query. That was the only place where Grid needed more code to match Flexbox.

**Which was more intuitive?**
Grid was more intuitive for the page structure. The area strings look like the wireframes in the brief, so you can read the layout straight from the CSS, and the tablet rule "sidebars become equal columns below the main content" is literally `"main main" "left right"` with `1fr 1fr`. Flexbox was more intuitive for content that should flow, like the navigation links and the cards, where we do not care which column an item lands in, only that it fits.

**When would we prefer one over the other?**
We would use Grid for the overall page skeleton whenever regions need to line up in two dimensions or move to different positions at different screen sizes. Level 3 showed that Grid scales well: adding a second sidebar only meant one more name in the map. We would use Flexbox inside those regions for one-dimensional groups such as menus, toolbars and card rows, especially when the last item should grow to fill the leftover space. Our final takeaway is that the two work best together: Grid for the layout, Flexbox for the components inside it.
