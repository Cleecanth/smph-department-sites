# Media queries and breakpoints management

This project uses a configuration variable (`$breakpoints`) and mixin (`media-query`) for its breakpoint management. For most of your needs, the `$breakpoints` map should be enough, but the `media-query` mixin is built with flexibility in mind.

## Simple examples

Let's assume you have two breakpoints within the `$breakpoints` variable.

```scss
$breakpoints: (
  mobile: '(max-width: 640px)',
  desktop: '(min-width: 641px)'
);
```

Referencing either of these is as simple as using the `media-query`, and passing in one of the named breakpoints.

```scss
@include media-query(mobile) {
  //code here..
}
```

You can also nest media queries within css declarations.

```scss
//SCSS
.foo {
  color: red;

  @include media-query(desktop) {
    color: blue;
  }
}

//Compiled CSS
.foo {
  color: red;
}

@media only screen and (min-width: 641px) {
  .foo {
    color: blue;
  }
}
```

## Recommendation

If you use a media-query more than once or twice, its recommended that you name it and add it to the `$breakpoints` map. However, sometimes you might need to a few breakpoints that are only applicable to a single layout or component (often called ["tweak points"](https://adactio.com/journal/6044)), so in those cases, it's recommended to pass "arbitrary" arguments to the mixin. These arbitrary arguments are explained down below.

## Advanced usage

### $breakpoints

In `_partials/scss/_config.scss`, you'll find a map variable that holds the names (keys) and media query values of a few pre-defined breakpoints. It's recommended that you not add too many key-value pairs, since the purpose of this variable is to _simplify_ your media-query management.

* Key - The name you'd like to give your media-query when referencing it from the `media-query` mixin.
* Value - The value you'd like to output. This should only be the media-query conditional that appears after `@media only screen and`.

The values you use should be based on your project, but the defaults are set up to work with most projects.

### media-query()

In `_partials/scss/globals/_media-queries.scss`, you'll find the mixin and its associated functions. A few required variables are also stored in `_partials/scss/globals/_private-vars.scss`, all name-spaced as `$media-query`. These variables are used as checks for valid media query expressions.

**Accepted arguments**

Other than the simple references from the `$breakpoints`, the mixin can accept arbitrary devices (`print`, `tv`, etc.), operators (`max-width`, `min-height`, etc.), and length values (`1px`, `25rem`, etc.). These should be separated by a space, and in that order (device, operator, length).

**Multiple, _OR_-based media queries**

Separating arguments by a comma indicates the creation of a separate media query. In the world of media queries, this is considered a logical **OR**.

```scss
@include media-query("min-width" 350px, mobile) {
  .foo {
    color: red;
  }
}
```

This, effectively creates two media queries, but for the sake of cleanliness, we can just append them with a comma, outputting this:

```scss
//Actual output
@media only screen and (min-width: 350px), screen and (max-width: 640px) {
  .foo {
    color: red;
  }
}
```

Which has the same effect as this:

```css
@media only screen and (min-width:350px) {
  .foo {
    color: red;
  }
}

@media only screen and (max-width:640px) {
  .foo {
    color: red;
  }
}

```

**Multiple, _AND_-based media queries**

Sass actually handles this for us by simply nesting media queries, so rather than repeating built-in behavior, the `media-query` mixin just gets out of Sass' way.

```scss
//Input
@include media-query("min-width" 350px) {
  @include media-query(mobile) {
    .foo {
      color: blue;
    }
  }
}

//Compiled
@media only screen and (min-width: 350px) and (max-width: 640px) {
  .foo {
    color: blue;
  }
}

```

## Grid interaction

In the configuration file, you'll find some variables (`$breakpoint-has-widths`, `$breakpoint-has-push`, `$breakpoint-has-pull`). More often than not, you'll want to list all of your named `$breakpoints` keys here. These tell the grid whether to generate classes based on these pairs.

**Class names**

Grid classes will inherit the names of your keys in `$breakpoints`. So, for instance, if you have your `$breakpoints` set up like the example at the top of this document, and you have `$breakpoints-has-widths: ('mobile', 'desktop')`, the grid will generate three classes (the extra class comes without any media query wrapper). Although these will generally be placeholder classes that go unseen, for the sake of simplicity, you will have access to classes like this:

```scss
%one_half { width: 50% }

@media only screen and (max-width: 640px) { //mobile
  %mobile_one_half { width: 50% }
}
@media only screen and (max-width: 641px) { //desktop
  %desktop_one_half { width: 50% }
}
```

The same logic applies to pushes and pulls (e.g. `%mobile_push_one_half`).
