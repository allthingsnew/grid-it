# Grid It

Provided is a stable (working) master copy of our in-house grid system. It's extremely easy to use for creating fast, robust resposive grids in HTML. It supports nested grids and doesn't require much CSS class tomfoolery to get things rolling. Base CSS classes are provided to use in the HTML markup along with SCSS mixins to use in your stylesheets offering the greatest amount of control.

The grid supports nested grids and needs no special, `.first`, `.last`, or `.end` classes!

For examples of how the grid works and best practices see the provided `style.scss` and `index.html` files.

## Variables

The grid system comes highly configurable from the number of columns to gutters to the base classes to be used. To alter these settings always copy the variables in your own settings/variables file *before* importing the grid. **Do not edit the grid file itself.**

Here are the variables you may modify with their default values:

```scss
$grid-cols: 12;  // [number] Number of columns in your grid
$grid-container-gutter: 85%;  // [css unit] Overall width of the page in the browser
$grid-max-width: 80em;  // [css unit] Maximum width of the page in the browser
$grid-breakpoint: 47em;  // [css unit] Only built-in breakpoint of the grid (everything flattens)
$grid-gutter: 2em;  // [css unit] Gutter between each column (negated on first and last columns)
$grid-container-class: container;  // [string] Base class of the container element
$grid-row-class: row;  // [string] Base class of each row
$grid-col-class: col;  // [string] Base class of each column
$grid-mobile-class: mobile;  // [string] Base class for mobile grid (is appended with -#)
$grid-mobile-cols: 4;  // [number] Number of cols in mobile grid
$grid-set-border-box: false !default;  // [bool] Set box-sizing on column classes (assumes applied globally by default)
```

## Base Classes

* `.container`: The container inside which your entire grid will reside.
* `.row`: The container to house columns.
* `.col`, `.cols`: Any column gets this class in conjunction with one of the number classes below.

*Note: these will match the names set in the variables above.*

**Row Extensions**

* `.half-gutter`: Renders all nested columns with half their gutter.
* `.collapse`: Collapses all nested column gutters. (affects only columns with base column class)

**Column Extensions**

* `.centered`: Used with a single column to center it within a row.

## Base Column Sizes

Column number classes from `.one` to as many as `.twentyfour` are provided (but will cap out at the number of columns the grid is set to). This would be used like so:

```html
<div class="row">
    <div class="eight cols"></div>
    <div class="four cols"></div>
</div>
```

## Offsets

If the case that you want to offset your columns by `x` number of columns you may use offset classes. These range from `.offset-1` up to `.offset-24`. However, they also are capped off at the number of columns the grid is set to.

## Source Ordering

If when you want to rearrange the order of columns independent of the markup push and pull classes are provided. These are just like offset in syntax, again ranging from `.push-1` and `.pull-1` to `.push-24` and `.pull-24`, capping off at the number of columns you set your grid.

## Mobile

Mobile classes are provided to retain a grid on mobile/handheld devices. Otherwise, grid columns will collapse vertically. Mobile classes are made up of the mobile class set in the above variables and number words like: `.mobile-one` to `.mobile-four` or whatever number of columns you set the mobile grid to.

You may also use mobile offsets and source ordering in the same manner as above. Mobile versions are prepended, like the number classes, with `mobile-` so these classes are like: `.mobile-offset-3`, `.mobile-push-4`, and `.mobile-pull-8`.

## Mixins

By using mixins you can tell any element in your project to look like a container, row, or column. Rows and columns come with some optional arguments. You may use them as follows:

```scss
//**
//* Create a container out of any element.
//*/
@mixin grid-container {
    //...
}

//**
//* Create a row out of any element.
//* @param {bool} $half-gutter Cut the gutter on each column within in half (acts on all direct decendents)
//* @param {bool} $collapse Remove the gutter on columns completely
//*/
@mixin grid-row($half-gutter: false, $collapse: false) {
    //...
}

//**
//* Create a column out of any element.
//* @param {num} $grid-cols Number of columns the element should span (default is max)
//* @param {num} $offset Number of columns the element should be offset by
//* @param {num} $push Push the element by x number of columns
//* @param {num} $pull Pull the element by x number of columns
//* @param {bool} $centered Center the column in the row (there should only be one)
//* @param {bool} $half-gutter Use only a half gutter on this specific column
//*/
@mixin grid-col($columns: $grid-cols, $offset: 0, $push: 0, $pull: 0, $centered: false, $half-gutter: false) {
    //...
}

//**
//* Add mobile grid to column.
//* @param {num} $mobile-cols Number of columns to span on mobiles (default is max)
//*/
@mixin grid-mobile($mobile-cols: $grid-mobile-cols) {
    //...
}

//**
//* Create column widths, offset, push, and pull classes within a given context.
//* @param {num} $num-cols The number of columns to build classes to
//* @param {string} $prepend A name to prepend to each grid class (a '-' separates this from the class name)
//*/
@mixin grid-classes($num-cols: $grid-cols, $prepend: false) {
    // any styles here are appended to each number class in the grid allowing for
    // deep customization of your grids.
}
```

**Tip**: Use [named arguments](http://sass-lang.com/docs/yardoc/file.SASS_REFERENCE.html#keyword_arguments) to make including much easier.

## Semantic Media Queries

You may extend the grid breakpoint included here by creating your own media queries and then building the grid classes within those queries using different grid schemas. To accomplish this utilize the `grid-classes` mixin like so:

```scss
// Creates a new 16-column grid with classes ranging from .bp2-one to .bp2-sixteen
@media only screen and (max-width: 60em) {
    @include grid-classes(16, bp2);
}
```

## Functions

You can use the funtion `gridCalc()` anywhere you need to in your scss files. It is used as follows:

```scss
//**
//* Calculate the percentage width by column span.
//* @param  {num} $colNumber The number of columns to span
//* @param  {num} (optional) $totalColumns The number to divide into (defaults to $grid-cols)
//* @return {num} CSS Percentage
//*/
@function gridCalc($colNumber, $totalColumns: $grid-cols) {
    //...
}
```

## Compatibility

Good ol' IE will give you some fits. IE8 and lower doesn't support media queries. IE7 and lower doesn't support `box-sizing`. The fixes are pretty simple and straightfoward though.

* Grab the resond.js polyfill to enable media queries [here](https://github.com/scottjehl/Respond).
* Use the box-sizing behavior polyfill for IE7 and lower [here](https://github.com/Schepp/box-sizing-polyfill).
