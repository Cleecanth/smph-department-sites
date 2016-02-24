# Sass Mixins

All mixins and functions can be found under the `scss/globals/` folder in `_mixins.scss` and `_media-queries.scss`.

## Mixins

#### rems( $property, $sizes, $important: false, $base-font: $base-font-size )

Takes a property and generates a `rem` value with a `px` value fallback. Can be used with any property and multiple sizes, as well as an optional `!important` flag.

** Arguments **
* `$property` - `string` : Any css property name (e.g. 'font-size').
* `$sizes` - `pixels (space-separated list)` : Pixel value(s) you'd like to be converted to rems.
* `$important` - `boolean` : Whether to append !important.
* `$base-font` - `pixels` : The pixel value used to calculate rem values against. Typically the font-size you have set on your body tag.


#### type-space( $properties, $multipliers, $important: false )

Takes a property, a list of multipliers, and generates a value based on the `$base-line-height` (vertical) or `$grid-gutter` (horizontal) settings. Useful for consistent spacing and/or heights and widths. Feeds calculations into [rems](#rems), returning values in rems (with pixel fallback).

** Arguments **
* `$property` - `string` : Any css property name (e.g. 'font-size').
* `$sizes` - `number (space-separated list)` : Multiple(s) to base calculations on. _For consistency, you should try to use increments of 0.5_.
* `$important` - `boolean` : Whether to append !important.


#### type-scale( $properties, $multipliers, $upper-limit: false, $important: false )

Similar to type-space, but based on the `$base-font-size` setting. Also allows for clamping using the `$upper-limit` argument. Feeds calculations into [rems](#rems), returning values in rems (with pixel fallback).

** Arguments **
* `$property` - `string` : Any css property name (e.g. 'font-size').
* `$sizes` - `number (space-separated list)` : Multiple(s) to base calculations on (multiplied by $base-font-size).
* `$upper-limit` - `pixels or false` : Forces multiplied values to never max out at this value. Useful in situations where your base font-size is in flux.
* `$important` - `boolean` : Whether to append !important.


#### clearfix( )

Applies a  the more modern version of the [micro clearfix](http://nicolasgallagher.com/micro-clearfix-hack/).


#### shadow( $z: 1, $inset: false )

Adds a box shadow with a baseline style that is used throughout the templates.

** Arguments **
* `$z` - `number` : An alias for the z-depth of the object you're applying the shadow to. Increments in the .1 - .5 range are recommended.
* `$inset` - `boolean` : Whether the box shadow should be inside or outside of the object.


#### media-query( $mq... )

##### Aliases: mq(), breakpoint(), bp()

To create more consolidated code, most (if not all) media queries
should be called through this mixin. Multiple media-queries can be defined, separated by a comma.
This will place your content into an **OR** media-query. This is useful if you need the same css at different breakpoints.

```scss
//Sass(scss):
@media-query(small, desk) {
  .selector{color: #fff}
}

//Compiled(css):
@media only screen and (max-width: 640px), screen and (min-width: 941px){
  .selector{color: #fff}
}
```

_Alternative Uses:_

* Passing a value like `min-width 120em` or `max-height 30px` allows for arbitrary breakpoints.

* Nesting media queries will create an **AND/chained** media-query. e.g. `@media-query(smalls){@media-query(bigs)}{ //Your Code here }`

* Media can be defined as well, like `@media-query(print max-width 8in)`. Screen is always assumed if no media type is defined.

** Arguments **
* `$mq` - `number or string` : A reference to a key in $breakpoints, or string and number combination like `"max-width" 250px`. Individual media-query arguments should be space-separated, while multiple should be separated by commas.

**For more detailed information, see [Media Query Management](media-queries.md).**
