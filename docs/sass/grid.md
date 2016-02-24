# Grid System

## Widths

The grid system built into this project is built with an 11-column base. All widths are calculated by dividing their own number by 11 (2/11 = 18.1818%).


## Rows and Columns

This particular grid-system, unless configured otherwise, uses `inline-block` for its columns, which comes with many benefits like being reversible and vertically-aligned. It also means you never have to clear or identify the last item in a row. Since `inline-block` behaves like type, your rows of columns can drop to the next line when necessary without any additional code.

The biggest drawback is that free-floating text is not allowed directly within a row. Because inline-block behaves like text, any spaces in your code are treated as spaces when rendered. We get around that by adding negative letter-spacing inside of rows.

A typical grid's markup would look like this:

```html
<div class="row">
  <div class="column c-3">
    <!-- content -->
  </div>
  <div class="column c-8">
    <!-- content -->
  </div>
</div>
```

### Rows

A row is identified simply with the class `row`. By default, the row will have a negative left margin that is equivalent to the grid's gutter width. This allows columns to drop to the next line without requiring extra markup. In a sense, a "row" is really just a grid-item-container with as many grid items as necessary. You can combine column widths and rows, but its recommended that you nest your rows and columns instead.

### Columns

Columns (identified with the `column` class) are, as stated before, `inline-block` elements. They have [`box-sizing: border-box`](https://developer.mozilla.org/en-US/docs/Web/CSS/box-sizing#Values) applied, and are given left padding equal to the grid's gutter. This allows all columns to sit next to each other without being aware of how many other columns they sit next to. This also offsets the negative margin applied to each row. Columns also reset the negative letter-spacing values applied by rows.

### Widths

Widths are identified with a `c-#` class that corresponds to a number out of 11. `<div class="column c-4">` would create a column with a width of 36.3636%. Since the widths are actually independent from the `column` class, they can be used on any item that needs a particular width. `c-4` will always add a width of 36.3636%, regardless of it being a column or not. Adding a `smalls-` before a column width's class name will give it a width that only applies to smaller screen sizes (mobile).

_Note: `c-half`, `c-third`, `c-quarter`, `c-two-thirds`, and `c-three-quarters` classes have been included for convenience. These should help where the 11-column grid might not be suitable._

### Pushes

Pushing columns allows you to position a column out of the natural flow of the grid. Using the `p-#` (where # is a number, similar to widths) class will move a column along the grid. Pushes share similar attributes as widths, but just applied to a `left` property.

### Nesting

All rows and columns can be nested. This allows for infinite combinations of widths and layouts. An example might be:
```html
<div class="row">
  <div class="column c-half">
    <div class="row">
      <div class="column c-8"></div>
      <div class="column c-3"></div>
    </div>
  </div>
  <div class="column c-half">
    <div class="row">
      <div class="column c-5"></div>
      <div class="column c-7"></div>
    </div>
  </div>
```

This would create a grid divided in two, but with inner columns with uneven widths.


---

## Advanced Usage

Here are a couple pre-written grid additions:

* **Tighter grid**: By adding `row-skinny` to any `row`, the columns gutter will be divided in half. A gutter-less row can be written like this:
```css
.row-flush { margin-left: 0; }
.row-flush > .column { padding-left: 0; }
```

* **Row Reset**: If you'd like a row that is essentially just a placeholder for nesting more rows, use the `columnRow` class. This will create a row that doesn't have a negative left margin, but still retains the rest of the necessary row attributes for columns and rows.


Taking advantage of the inline-block nature of the grid system, we can do a number of things a float-based grid would have a difficult time with. Here are some examples:

* **Vertically-centered columns**: By adding `row-middle` to any `row`, the columns within the row will be centered along their vertical axis. A _bottom-aligned_ row can be written like this:
```css
.row-bottom > .column { vertical-align: bottom; }
```

* **Reversed Row**: A row where grid items start at the right and move left. Although not included in the provided css, it can be added using this:
```css
.row-reversed { direction: rtl; text-align: left; }
.row-reversed > .column { direction: ltr; }
```

Any of these attributes can be combined with each other since they are completely modular. An impractical, but possible, example:

```html
<div class="row row-skinny row-reversed row-middle">
  <div class="column c-4 smalls-c-quarter">
    <!--content-->
  </div>
  <div class="column c-5 smalls-c-quarter smalls-p-half">
    <!--content-->
  </div>
  <div class="column c-2 smalls-c-quarter smalls-p-quarter">
    <!--content-->
  </div>
</div>
```

[Here's a demo of how this would render](http://codepen.io/Cleecanth/pen/LGBWeQ?editors=1100).

---

## Under the Hood

Column widths within `/_partials/scss/components/_columns.scss` are built by extending placeholder classes generated by mixins within `/_partials/scss/globals/_grid.scss`. The silent classes are named like so:

```scss
%[media-query-name]_[numerator]_[denominator]

//Example names
%one_fourth {}
%small_one_tenth {}
%desk_six_elevenths {}
```

The `grid-init` mixin returns three other mixins: `grid-setup`, `width-setup`, `push-setup`, and `pull-setup`. It iterates over these mixins based on the settings of `$breakpoint-has-[widths | pulls | push]`.

* `grid-setup` creates the initial row (`%grid`) and column (`%grid_item`) classes.

* `width-setup` creates human-readable grid class names for widths.

* `push-setup` creates human-readable grid class names for pushes.

* `pull-setup` creates human-readable grid class names for pulls.


**See the Grid Interaction portion of the [Managing media queries documentation](media-queries.md) for more details.**
