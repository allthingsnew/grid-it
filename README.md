# [Grid-It v2.0.2](http://allthingsnew.github.com/grid-it/)

Grid-It is a CSS grid system built from the best practices of several other grid systems. It benefits from using the best points of other CSS grid philosophies without being tied to their complete systems. It aims at being as lightweight as possible and as powerful as possible. Grid-It rests on the following strengths:

* Border Box Sizing
* Mobile-First Development
* Fixed Gutters Based on Font Size
* Full Semantic Control

To see Grid-It in action be sure to check out our [demo page](http://allthingsnew.github.com/grid-it/).

## Installation & Usage

To get started do one of the following:

* [Download the current version here.](https://github.com/allthingsnew/grid-it/archive/2.0.2.zip)
* Clone this repo: `git clone git://github.com/allthingsnew/grid-it.git`
* Fork our repo and play with it!

Grid-It is contained in a single Sass file! Just place `_grid-it.scss` in your project directory and import it before your grid classes. Edit the default settings by writing the applicable variables in your project before including Grid-It.

## Variables

Grid-It comes highly configurable from the number of columns to gutters to the base classes to be used. To alter these settings always copy the variables in your own settings/variables file *before* importing the grid. **Do not edit the grid file itself.**

Here are the variables you may modify with their default values:

| Variable Name | Default Value | Description |
| ------------- | ------------- | ----------- |
| $grid-cols | 12 | Total columns in your grid |
| $grid-container-gutter | 85% | Overall width of the grid |
| $grid-max-width | 90em | Maximum width of the grid |
| $grid-breakpoint | 47em | When mobile grid switches to desktop |
| $grid-gutter | 1em | Gutter between each column |
| $grid-container-expand | false | Expand containers to the full width on mobiles |
| $grid-container-class | container | Classname of container elements |
| $grid-row-class | row | Classname of rows elements |
| $grid-col-class | col | Classname of column elements |
| $grid-mobile-class | mobile | Prefix for all mobile classes |
| $grid-mobile-cols | 4 | Number of mobile grid columns |
| $grid-set-border-box | false | Set border-box on column elements |

## Base Classes

* `.container`: The container inside which your entire grid will reside.
* `.row`: The container to house columns.
* `.col`, `.cols`: Any column gets this class in conjunction with one of the number classes below.

*Note: these will match the names set in the variables above.*

**Extensions**

| Class | Extends | Description |
| ----- | ------- | ----------- |
| `.half-gutter` | Row | Renders all nested columns with half their gutter. |
| `.collapse` | Row | Collapses all nested column gutters. |
| `.centered` | Column | Centers a single column in a row. |

## Column Spans

Grid-It creates number classes from `.one` to as many as `.twentyfour`. They stop at what `$grid-cols` is set to. Their use is straightforward:

```html
<div class="row">
    <div class="eight cols"></div>
    <div class="four cols"></div>
</div>
```

## Offsets

Grid-It makes offsetting your columns a cinch. Provided are offest classes that range from `.offset-1` up to `.offset-24`. Again, these are capped off at the number set in `$grid-cols` to save space in your css file.

## Source Ordering

Every now and then we need to rearrange the order of columns independent of the markup. This is why Grid-It provides push and pull classes. These are just like offset in syntax, again ranging from `.push-1` and `.pull-1` to `.push-24` and `.pull-24`, ending at `$grid-cols`.

## Mobile

How about a grid on mobile/handheld devices? You got it! Mobile classes are made up of the mobile class set in the above variables and number words like: `.mobile-one` to `.mobile-four` or whatever number of columns you set in `$grid-mobile-cols`.

You may also use mobile offsets and source ordering in the same manner described above. Mobile classes are prepended, like the number classes, with `.mobile-` (see `$grid-mobile-class`) so these classes are like: `.mobile-offset-3`, `.mobile-push-4`, and `.mobile-pull-8`.

From time to time different column groups are also needed between mobile and desktop grids. For this reason `.mobile-row` is provided. This is a class given to elements that wrap mobile columns and looks like a row on mobile but becomes lax on after the grid breakpoint. Nest these elements within common rows to achieve complex grid grouping.

## Semantics

Grid-It is a semantic grid, meaning that while it comes with every class needed out of the box it's built atop a library of mixins you can use to tell any element to look like a grid component.

### Mixins

| Syntax | Description | Options |
| ------ | ----------- | ------- |
| @include grid-container; | Create a container. | none |
| @include grid-row( *opts* ); | Create a row. | $half-gutter: false <br> $collapse: false |
| @include grid-col( **#**, *opts* ); | Create a column | **$columns: #** <br> $offset: 0 <br> $push: 0 <br> $pull: 0 <br> $centered: false <br> $half-gutter: false <br> $mobile-cols: 0 |
| @include grid-classes( **#**, *opts* ); | Create a new grid w/ prepended name | **$num-cols: #** <br> $prepend: false |

__*Required arguments in bold type.__

**Tip**: Use [named arguments](http://sass-lang.com/docs/yardoc/file.SASS_REFERENCE.html#keyword_arguments) to make including much easier.

### Grid Classes

To extend the single breakpoint built into Grid-It use the mixin `grid-classes()` within a media query. You can overwrite the grid at this new breakpoint or supply an alternative grid system by giving the mixin a prepend name as its secondary parameter. For example:

```scss
@media only screen and (min-width: 60em) {
    @include grid-classes(16, bp2);
}
```

This creates a new 16-column grid effective at min-width: 60em with classes prepended with `.bp2-` like `.bp2-one`, `.bp2-pull-3`, `.bp2-offset-6`, etc.

## Functions

The funtion `gridCalc()` is provided to be used anywhere you need to calculate the percentage of a span within a given number of columns. The first argument is required. The second argument defaults to `$grid-cols`. For example:

```scss
header {
    width: gridCalc(4, 16);  // 25%
}
```

We've also included a helper clearfix mixin used like `@include clearfix;`. It simply clears the height of anything that contains floated elements.

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
