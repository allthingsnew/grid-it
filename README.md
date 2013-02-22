# [Grid-It v2.0.2](http://allthingsnew.github.com/grid-it/)

Grid-It is a CSS grid system built from the best practices of several other grid systems. It benefits from using the best points of other CSS grid philosophies without being tied to their complete systems. It aims at being as lightweight as possible and as powerful as possible. Grid-It rests on the following strengths:

* Border Box Sizing
* Mobile-First Development
* Fixed Gutters Based on Font Size
* Full Semantic Control

## Installation & Usage

To get started do one of the following:

* [Download the current version here.](https://github.com/allthingsnew/grid-it/archive/2.0.2.zip)
* Clone this repo: `git clone git://github.com/allthingsnew/grid-it.git`
* Fork our repo and play with it!

Grid-It is contained in a single Sass file! Just place `_grid-it.scss` in your project directory and import it before your grid classes. Edit the default settings by writing the applicable variables in your project before including Grid-It.

## Variables

Grid-It comes highly configurable from the number of columns to gutters to the base classes to be used. To alter these settings always copy the variables in your own settings/variables file *before* importing the grid. **Do not edit the grid file itself.**

Here are the variables you may modify with their default values:

```scss
// Number of columns in your grid
$grid-cols: 12;

// Overall width of the page in the browser
$grid-container-gutter: 85%;

// Maximum width of the page in the browser
$grid-max-width: 80em;

// Only built-in breakpoint of the grid (everything flattens)
$grid-breakpoint: 47em;

// Gutter between each column (negated on first and last columns)
$grid-gutter: 1em;

// Base class of the container element
$grid-container-class: container;

// Should containers expand to full-width on mobile
$grid-container-expand: false;

// Base class of each row
$grid-row-class: row;

// Base class of each column (is also pluralized)
$grid-col-class: col;

// Base class for mobile grid (is appended with -#)
$grid-mobile-class: mobile;

// Number of cols in mobile grid
$grid-mobile-cols: 4;

// Set box-sizing on column classes
// If false, set globally
$grid-set-border-box: false;
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

Column number classes from `.one` to as many as `.twentyfour` or whatever `$grid-cols` is set to. This would be used like so:

```html
<div class="row">
    <div class="eight cols"></div>
    <div class="four cols"></div>
</div>
```

## Offsets

If the case that you want to offset your columns by `x` number of columns you may use offset classes. These range from `.offset-1` up to `.offset-24` (or whatever `$grid-cols` is set to).

## Source Ordering

If when you want to rearrange the order of columns independent of the markup use push and pull. These are just like offset in syntax, again ranging from `.push-1` and `.pull-1` to `.push-24` and `.pull-24`, ending at `$grid-cols`.

## Mobile

Mobile classes are provided to produce a grid on mobile/handheld devices. Otherwise, grid columns are collapsed vertically. Mobile classes are made up of the mobile class set in the above variables and number words like: `.mobile-one` to `.mobile-four` or whatever number of columns you set the mobile grid to.

You may also use mobile offsets and source ordering in the same manner as above. Mobile versions are prepended, like the number classes, with `mobile-` so these classes are like: `.mobile-offset-3`, `.mobile-push-4`, and `.mobile-pull-8`.

From time to time different column groups are also needed between mobile and desktop grids. For this reason `.mobile-row` is provided. This is a class given to elements that wrap mobile columns and looks like a row on mobile but becomes lax on after the grid breakpoint. Nest these elements within common rows to achieve complex grid grouping.

## Semantics

Grid-It is a semantic grid, meaning that while it comes packed with every class needed you can use it's own mixins library to tell any element to look like a grid component. Use them as follows:

```scss
// Create a container out of any element.

@include grid-container;


// Create a row out of any element.
// @param {bool} $half-gutter Cut the gutter on each column within in half (acts on all direct decendents)
// @param {bool} $collapse Remove the gutter on columns completely
// @param {bool} $has-mobile Whether or not the row contains mobile columns

@include grid-row();


// Create a column out of any element.
// @param {num} $columns Number of columns the element should span (required)
// @param {num} $offset Number of columns the element should be offset by
// @param {num} $push Push the element by x number of columns
// @param {num} $pull Pull the element by x number of columns
// @param {bool} $centered Center the column in the row (there should only be one)
// @param {bool} $half-gutter Use only a half gutter on this specific column
// @param {num} $mobile-cols Number of columns to span on mobile, if any

@include grid-col($columns);


// Create column widths, offset, push, and pull classes within a given context.
// @param {num} $num-cols The number of columns to build classes to (required)
// @param {string} $prepend A name to prepend to each grid class (a '-' separates this from the class name)

@include grid-classes($num-cols) {
    // any styles here are appended to each number class in the grid
}
```

**Tip**: Use [named arguments](http://sass-lang.com/docs/yardoc/file.SASS_REFERENCE.html#keyword_arguments) to make including much easier.

## Semantic Media Queries

You may extend the grid breakpoint included here by creating your own media queries and then building the grid classes within those queries using different grid schemas. To accomplish this utilize the `grid-classes` mixin like so:

```scss
// Creates a new 16-column grid with classes ranging from .bp2-one to .bp2-sixteen
@media only screen and (min-width: 60em) {
    @include grid-classes(16, bp2);
}
```

## Functions & Mixins

You can use the funtion `gridCalc()` anywhere you need to in your scss files. It is used as follows:

```scss
// Calculate the percentage width by column span.
// @param  {num} $colNumber The number of columns to span
// @param  {num} (optional) $totalColumns The number to divide into (defaults to $grid-cols)
// @return {num} CSS Percentage

gridCalc($colNumber, $totalColumns: $grid-cols);
```

Also provided is a mixin to clearfix elements. Simply use it like:

```scss
@include clearfix;
```

## Browser Compatibility

Legacy IE will throw some fits. IE8 and lower doesn't support media queries. IE7 and lower doesn't support `box-sizing`. The fixes are pretty simple and straightfoward though.

* Grab the [resond.js polyfill](https://github.com/scottjehl/Respond) to enable media queries (IE8).
* Use the [box-sizing behavior polyfill](https://github.com/Schepp/box-sizing-polyfill) for IE7 and lower.

## Copyright & Licenses

Copyright 2013 Multiversal Enterprises, LLC.

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this work except in compliance with the License.
You may obtain a copy of the License in the LICENSE file, or at:

  [http://www.apache.org/licenses/LICENSE-2.0](http://www.apache.org/licenses/LICENSE-2.0)

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
