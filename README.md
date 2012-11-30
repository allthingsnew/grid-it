# Grid It

Provided is a stable (working) master copy of our in-house grid system. It's extremely easy to use for creating fast, robust resposive grids in HTML. It supports nested grids and doesn't require much CSS class tomfoolery to get things rolling. Base CSS classes are provided to use in the HTML markup along with SCSS mixins to use in your stylesheets offering the greatest amount of control.

The grid supports nested grids and needs no special, `.first`, `.last`, or `.end` classes!

For examples of how the grid works and best practices see the provided style.scss and index.html files.

## Install

Simply place the _grid.scss file somewhere in your project and import (near the top).

## Use

### Variables

The grid system comes highly configurable from the number of columns to gutters to the base classes to be used. To alter these settings always copy the variables in your own settings/variables file *before* importing the grid. **Do not edit the grid file itself.**

Here are the variables you may modify with their default values:

    $grid-cols: 12;  // [number] Number of columns in your grid
    $grid-container-gutter: 85%;  // [css unit] Overall width of the page in the browser
    $grid-max-width: 80em;  // [css unit] Maximum width of the page in the browser
    $grid-breakpoint: 48em;  // [css unit] Only built-in breakpoint of the grid (everything flattens)
    $grid-gutter: 2em;  // [css unit] Gutter between each column (negated on first and last columns)
    $grid-container-class: container;  // [string] Base class of the container element
    $grid-row-class: row;  // [string] Base class of each row
    $grid-col-class: col;  // [string] Base class of each column
    $grid-set-border-box: true;  // [bool] Set box-sizing on column classes (turn off if applied globally)

### Base Classes

* `.container`: The container inside which your entire grid will reside.
* `.row`: The container to house columns.
* `.col`: Any column gets this class in conjunction with one of the number classes below.

### Base Column Sizes

Column number classes from `.one` to as many as `.twentyfour` are provided (but will cap out at the number of columns the grid is set to). This would be used like so:

    <div class="row">
        <div class="eight col"></div>
        <div class="four col"></div>
    </div>

### Offset

If the case that you want to offset your columns by `x` number of columns you may use offset classes. These are prefixed with `offset-` and range from `.offset-1` up to `.offset-24`. However, they also are capped off at the number of columns the grid is set to.

### Push & Pull

In those instances when you may want to reverse the order of two columns *without* editting the markup push and pull classes are provided. These are just like offset in syntax, again ranging from `.push-1` and `.pull-1` to `.push-24` and `.pull-24`, capping off at the number of columns you set your grid.

### Mixins

By using mixins you can tell any element in your project to look like a container, row, or column. Rows and columns come with some optional arguments. You may use them as follows:

    /**
     * Create a row out of any element.
     * @param {bool} $half-gutter Cut the gutter on each column within in half (acts on all direct decendents)
     * @param {bool} $collapse Remove the gutter on columns completely
     */
    @mixin grid-row($half-gutter: false, $collapse: false) {
        //...
    }

    /**
     * Create a column out of any element.
     * @param {num} $grid-cols Number of columns the element should span (default is max)
     * @param {num} $offset Number of columns the element should be offset by
     * @param {num} $push Push the element by x number of columns
     * @param {num} $pull Pull the element by x number of columns
     * @param {bool} $centered Center the column in the row (there should only be one)
     * @param {bool} $half-gutter Use only a half gutter on this specific column
     */
    @mixin grid-col($columns: $grid-cols, $offset: 0, $push: 0, $pull: 0, $centered: false, $half-gutter: false) {
        //...
    }

**Tip**: Use [named arguments](http://sass-lang.com/docs/yardoc/file.SASS_REFERENCE.html#keyword_arguments) to make including much easier.