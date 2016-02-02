# Sass

## Configuration (/\_partials/scss/\_config.scss)

### Typography

* **$base-font-size** (pixel value):  Base value for all font-sizes. This will be used as a percentage value on the `html` tag. From there all values will be calculated in `rems`, using this value as their context.
  * Default: `12px`

* **$base-line-height** (pixel value): Base value for `line-height` on your document. This will also determine the vertical space that is calculated by the `type-space` mixin.
  * Default: `12px`

* **$rem-px-fallback** (boolean): When calculating `rems`, determine whether pixel values should also be output. This is typically only necessary for IE8. _Fallbacks will not be added inside media-queries._
  * Default: `true`


### Colors

* **Base colors**: Included as a reference point and, based on branding standards, shouldn't be changed. They are here for mostly for transparency and developer convenience.

* **Theme colors**

  * **$color-main-bg**: The background color behind the standard page. For consistency across departments, your footer color will be automatically calculated based on this value.
    * Default: `$smph-gold`

  * **$color-main-nav**: Navigation bar color. This color should only be changed after careful consideration as it provides much of the balance to your pages and logo.
    * Default: `$badger-red`

  * **$color-pod-top**: Color for primary pod and news ticker headers. Again, changing this should be done with careful consideration since these also provide page balance.
    * Default: `$badger-red`


### Grid

**For a full explanation of the grid system included in this project, see the [grid documentation](grid.md).**

Most of these variables role's are straightforward and are explained in the comments, but here are a few that require some extra explanation:

* **$grid-gutter** (pixel value): This number is used when horizontal units are given to the `type-space` mixin.
  * Default: `24px`

* **$grid-silent-classes** (boolean): The grid system will generate classes across all breakpoints defined in $breakpoint-has-widths, $breakpoint-has-push, and $breakpoint-has-pulls, but by making them silent, we can just extend them as necessary (as you see in [columns.scss](../../_partials/scss/components/_columns.scss)). If this is set to `false`, the grid mixin will generate 55 classes (times the number of breakpoints) as CSS-visible classes. While this is nice automation, it's probably overkill for most projects.
  * Default: `true`

* **$grid-margin-adjustments** (boolean): The grid defaults to `relative` positioning to slide grid items around. This is preferable in most cases, since it doesn't affect the natural box flow, but this may not be your preference. If you are using a float-based grid, this becomes a more important question.
  * Default: `false`

### Media Queries

**For a full explanation of the sass media-query management in this project, see the [media query documentation](media-queries.md).**

* **$breakpoints** (map): Store pre-defined media-queries here, with their names being the keys and the media query conditions being the values. The values can be called upon by using the `media-query` mixin. Key names should be memorable, while values should be useful within the context of your project.

* **$brekpoint-has-widths** (list): A list of media-query names listed in your `$breakpoints` that will have grid-width values available.

* **$brekpoint-has-push** (list): A list of media-query names listed in your `$breakpoints` that will have grid-pushes values available.

* **$brekpoint-has-pull** (list): A list of media-query names listed in your `$breakpoints` that will have grid-pull values available.

Examples for `$breakpoints` and `$breakpoint-has-[widths | push | pull]`:

```scss
//Config code
$breakpoints: (
  'smalls': '(max-width:684px)',
  'desk': '(min-width: 685px)'
);

$breakpoint-has-widths: ('smalls', 'desk');
$breakpoint-has-push: ('smalls', 'desk');

//Component code
.component {
  @extend %smalls_one_whole;
  @extend %desk_one_half;
  @extend %desk_push_one_half;
}

//Compiled CSS output
@media only screen and (max-width:684px) {
  .component {
    width: 100%;
  }
}

@media only screen and (min-width:685px) {
  .component {
    width: 50%;
    left: 50%;
  }
}
```

As you can see, the component was placed into two different media queries in the compiled CSS, but its code within the SCSS was neatly kept under a single class. This makes your Sass much easier to read and maintain.

For more advanced media-query management, see the [media query documentation](media-queries.md).
