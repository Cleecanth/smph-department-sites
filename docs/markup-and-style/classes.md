# General class structure and style

The markup of pages is built with modularity in mind. Most HTML tags are appended with at least one class, and most styles are built to work alone, but with a mind toward being combined.

A simple example is the `page` and `wrapper` classes you see peppered throughout the project. `page` adds a white background and a box-shadow, while `wrapper` sets the site's container styles (a max-width and "auto" horizontal margins). These two classes can work independently of each other, but are often combined to create the main background of a page. For instance, if you wanted to create a card-like element, you could combine `page` with another class that adds a border and an overflow. The point being, the class name "page" is really representative of a page or paper-like element, other classes can handle various interpretations of what type of "page" it is.

**Simple Example**

Let's say you wanted to give some primary pods blue backgrounds. You could then create a class like `.bgBlue {background-color: blue}`. You could then mark up it up like so: `<div class='primaryPod-body bgBlue'>`. This would not only let you change your primary pods, but also apply this new class to other items on your project.

## Class naming convention

For legacy reasons, not all class names are perfectly structured, but they generally follow a similar structure:

`[parentElement]-[childElement]-[modifier]`

As an example, see the `primaryPod` class. This component has a wrapper(`parentElement`), and children elements (`childElement`) like `primaryPod-head` or `primaryPod-body`. this is preferable to using parent-child selectors (`.parent .child`) because it keeps the specificity of the CSS low, and allows for additional classes to be added to the html if special modification is necessary (`<div class="primaryPod-body padT10"` to add some additional padding to the top of the body).

## Utility classes

At the bottom of the main stylesheet, you'll find a group of single-use classes with an `!important` flag. These are typically referred to as "utility" classes. They exist solely to modify and override existing component styles, and are always "low impact". They typically only affect one style property, and essentially fill in the gaps where components/modules might fall short. Instead of writing a new class for a component that only appears slightly different from the default styling, these utility classes can be plugged in. If you find yourself using 3 or more of these on a single item, it might be worth writing a new component class. Finding the balance between too many utility classes and components often comes down to preference.
