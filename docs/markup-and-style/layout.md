# Layout and grid style reference

There are only a few crucial (but flexible) layout classes built into this project.

### Layout classes

For the sake of explanation, We'll make a distinction from grid (columns and rows) and layout classes. Layout, in this case, refers to the larger structures of a page. In architectural terms, you can think of these classes as the foundation, frame, and roof (while the grid would be more like the walls). _These classes are largely unique, without much opportunity for re-use._

*  `wrapper`: Constrains the page to your site's maximum width (default: 940px) and centers the site on the page.

* `top`: The very top of the page. Adds a gradient to the background, and raises the z-index above the nav bar.

* `logo`, `logo-crest`, `logo-type`: Highly specialized for the main department logo and crest. All children of `logo` are sized with `em` units, based on the font-size set by `logo`. Changing the font-size on logo will scale all children.

* `top-nav`: A container for the utility navigation. On desktop, aligns items to the right with a white background; On mobile, blends itself into the nav-bar and holds the "Menu" and "Search" buttons.

* `navBar`, `navBar-items`: The larger, main navigation for the site. Contains a few breakpoints that change the display of the nav items depending on the screen size. Hidden on smaller screens until the "menu" button is activated.

* `leftNav`, `leftNav-items`: Container for section navigation. Layout is controlled by flexbox on smaller screens, positioning it above the main content of the page.

* `footer`: Wrapper for the page's final tier of content. Adds a complementary background color, shrinks the font-size by 10%, and moves itself over the top of the main page content with a negative top margin.

### Specialized layout classes

* `media`: Keeps media and adjoining text from wrapping, while staying connected. Useful for bios, icons, or comment formatting. Only useful for a single image and a single block of text. You can see a demonstration of this at the bottom of the [example page](http://uwhealth.github.io/smph-department-sites/).

* `arrange`: Similar to `media`, but with the ability to vertically align content and have any number of "columns". You can see an example of this on with the logo at the top of the [example page](http://uwhealth.github.io/smph-department-sites/).

## Grid classes

 The grid is mainly made up of two classes: `row` and `column`. Widths and positioning are controlled by classes with a `c-#`, and `p-#`. For a more detailed explanation, see [the grid documentation](../sass/grid.md).

 * `row`: Container for `columns`. Adds a negative left margin. Columns should always be wrapped with a `row`.

 * `column`: Column module. Should be accompanied by a width modifier (defaults to 100%).

 * `c-#`: Changes the width of a column (or row). The `#` should be replaced by a number from 1-11. All numbers are divided by 11 to create their percentage.

 * `p-#`: Moves a column to the right by a grid increment. The `#` should be replaced by a number from 1-11. All numbers are divided by 11 to create their percentage.

### Specialized grid classes

 * `bodyContent`: Specialized column for the main content of the page.

   * `bodyContent-article`, `bodyContent-aside`: Complementary column modifiers with a 3:1 ratio on larger screens. Stacked on smaller screens.

   * `bodyContent-article-wide`, `bodyContent-aside-thin`: Similar to the above, but with a 4:1 ratio on larger screens.
