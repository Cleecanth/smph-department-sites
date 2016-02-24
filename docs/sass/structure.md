# Sass file and folder structure

In general, the structure of this project is set up in a way that as more files are imported, CSS specificity increases. Each folder's set of files has a specificity that is one (or more) higher than the previously imported. Generally, this allows projects to grow in an organic way without conflicts. Here's how it breaks down:

1. **globals** (_0 specificity_): Sass-specific functions, variables, and mixins. Should not actually produce any CSS.

2. **base** (_+1 specificity_): Tag-based styles and browser resets. These styles should never apply to classes.

3. **components** (_+2 specificity_): Class-based styles, making up the bulk of the project. Generally only single-classed components and modifiers. Built in the [OOCSS](https://www.smashingmagazine.com/2011/12/an-introduction-to-object-oriented-css-oocss/) style, where each component is responsible for itself, working independently of other classes, with a mind toward being combined to create variety. These components are kept within their own files that generally correspond to `.kit` files of the same name.

    - **components/header**: Broken out mostly for organization, but generally follows the same principle as everything within components.

4. **theme** (_+3 specificity_): Scoped class styles, specific to particular pages or larger project-specific items. Typically involves parent-child relationships (e.g. `.home .banner {...}`). If the project defaults work as expected, you can place most of your additional styles here.

5. **utilities** (_Infinite specificity_): Override/utility classes. Meant to be used as a way to control layout and modify default component styling. Although the single-class specificity is technically low, most of these classes are flagged with `!important` to ensure they work no matter their context. Classes should only be added to this when a component is insufficient.

**"Glob" Imports**

Since Sass does not support "glob" imports, `base` and `components` have their own `_import.scss` files that import files from their respective folders. These simply exist to make the process of adding new files a little cleaner.
