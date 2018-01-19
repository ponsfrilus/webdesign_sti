<!-- DOC https://hackmd.io/s/NJhm2CHEx# -->
<!-- Authors: @loichu & @ponsfrilus -->


<!-- .slide: data-background="http://instaco.de/stream/114913"-->
# WebSTI
## —&nbsp;developing&nbsp;the&nbsp;theme&nbsp;—

----

# Purpose

> The purpose of this presentation is to present the tools we use (or can use) in the development process for the new School of Engineering website's WordPress theme.

---

## Side note

This document has been made with <hackmd.io> and can be displayed as ([reveal.js](https://github.com/hakimel/reveal.js/)) slides here: https://hackmd.io/p/H1yB28iEM#/

---

# List of tools

* npm - <https://www.npmjs.com/>
* gulp - <https://gulpjs.com/>
* sass - <http://sass-lang.com/>
* browsersync - <https://browsersync.io/>
* bootstrap 4 - <https://v4-alpha.getbootstrap.com/>

---

# npm

![npm_logo](https://upload.wikimedia.org/wikipedia/commons/thumb/d/db/Npm-logo.svg/640px-Npm-logo.svg.png)

---

## Build amazing things

* npm is the package manager for JavaScript.
* Use npm to install, share, and distribute code; manage dependencies in your projects; and share & receive feedback with others.

---

## Where do we use npm ? (1/2)

* We are using `node_modules` for a lot of JS related stuff. For example, we use it for importing bootstrap, fontawesome, jquery, cookieconsent, etc.
* The full list stand in `package.json` in the `epfl-sti` theme folder.

---

## Where do we use npm ? (2/2)

* When we run `npm i` (or `npm install`), all the package listed in `package.json` are downloaded and installed into the `node_modules` folder.

---

# gulp

![gulp_logo](https://github.com/gulpjs/artwork/blob/master/gulp-cover.png?raw=true)

---

## Automate and enhance your workflow

* gulp is a toolkit for automating painful or time-consuming tasks in your development workflow, so you can stop messing around and build something. 

---

## Where do we use gulp ?

* When we run `npm`, the `postinstall` command in `package.json` call `gulp` and execute the content of `gulp.js`.
* When called, it:
    * process the `sass` files;
    * unify and unglify `css` and `js` files;
    * create minified images.

---

# sass

![sass_logo](http://sass-lang.com/assets/img/logos/logo-b6e1ef6e.svg)

---

## CSS with superpowers 

* Sass is the most mature, stable, and powerful professional grade CSS extension language in the world.

---

## Sass makes CSS fun again

* Sass is an extension of CSS, adding nested rules, variables, mixins, selector inheritance, and more.

* The main syntax (as of Sass 3) is known as "SCSS" (for "Sassy CSS"), and is a superset of CSS's syntax. This means that every valid CSS stylesheet is valid SCSS as well. SCSS files use the extension `.scss`.

---

## Where do we use sass ?

* When we run `npm`, the `postinstall` command in `package.json` call `gulp` and execute the content of `gulp.js` which compiles the theme's SCSS files (located in the `sass` folder) to CSS files.

---

## Sass example (variables)

```css
body {
  font: 100% Helvetica, sans-serif;
  color: #333;
}

```
is the same as:
```sass
$font-stack:    Helvetica, sans-serif;
$primary-color: #333;

body {
  font: 100% $font-stack;
  color: $primary-color;
}

```

---

## Sass example (nesting)

```css
nav ul {
  margin: 0;
  padding: 0;
  list-style: none;
}

nav li {
  display: inline-block;
}

nav a {
  display: block;
  padding: 6px 12px;
  text-decoration: none;
}
```

---

is the same as:
```sass
nav {
  ul {
    margin: 0;
    padding: 0;
    list-style: none;
  }

  li { display: inline-block; }

  a {
    display: block;
    padding: 6px 12px;
    text-decoration: none;
  }
}

```

---

## Sass example (import)

CSS has an import option but each time you use @import in CSS it creates another HTTP request. Sass builds on top of the current CSS @import but instead of requiring an HTTP request, Sass will take the file that you want to import and combine it with the file you're importing into so you can serve a single CSS file to the web browser.

```sass
// base.scss

@import 'color_variables';
```
*Note the missing `.scss` file extentions*

---

## Sass example (extends)
```css
.message, .success, .error, .warning {
  border: 1px solid #cccccc;
  padding: 10px;
  color: #333;
}
.error {
  border-color: red;
}
...
```

```sass
%message-shared {
  border: 1px solid #ccc;
  padding: 10px;
  color: #333;
}
.error {
  @extend %message-shared;
  border-color: red;
}
...
```
*Note the missing `.scss` file extentions*

---

# BrowserSync
![BrowserSync_logo](https://www.browsersync.io/brand-assets/wordmark-red.png)

---

## Time-saving synchronised browser testing.

* From live reloads to URL pushing, form replication to click mirroring, Browsersync cuts out repetitive manual tasks. It’s like an extra pair of hands.

---

## When to use BowerSync ?

* When developing the theme, use `npm start` to let `BrowserSync` refresh your browser when `gulp` has finished its works.

---

# Bootstrap

![bootstrap_logo](https://s3.amazonaws.com/coursetro/course_images/16_thumb.jpg)

Showcase: *https://loichu.github.io/Bootstrap4-Showcase/*

---

## Why Bootstrap

* Fast development
* Flexibility
* Big community

---

## Basics

* Grid part and raw components part
* Containers and rows
* Latest css features embeded

*http://getbootstrap.com/docs/4.0/layout/overview/*

---

## Grid layout

* **12**, the golden number
* Responsive design
* Nesting grids
* Offsets

*http://getbootstrap.com/docs/4.0/layout/grid/#how-it-works*

----

A row made of one column at 50% of the screen surrounded by two automatic width columns.
```htmlmixed=
<div class="container">
  <div class="row">
    <div class="col">
      1 of 3
    </div>
    <div class="col-6">
      2 of 3 (wider)
    </div>
    <div class="col">
      3 of 3
    </div>
  </div>
</div>
```

----

# Responsive breakpoints

There are five grid tiers, one for each responsive breakpoint: 
* all breakpoints (extra small) `xs`, 
* small `sm`, 
* medium `md`, 
* large `lg`, 
* and extra large `xl`.

*https://v4-alpha.getbootstrap.com/layout/grid/#grid-options*

----

The first and third columns will disappear on small screens and the second one will take the full width. Thanks to the display property wrapper (d-).
```htmlmixed=
<div class="container">
  <div class="row">
    <div class="col d-sm-none d-md-block">
      1 of 3
    </div>
    <div class="col-md-8 col-sm-12">
      2 of 3 (wider)
    </div>
    <div class="col d-sm-none d-md-block">
      3 of 3
    </div>
  </div>
</div>
```
*https://getbootstrap.com/docs/4.0/utilities/display/*

----

We can make a smaller column for small screens with an offset to keep it centered. 
Or better: horizontal alignment (next slide...)

```htmlmixed=
<div class="container">
  <div class="row">
    <div class="col d-sm-none d-md-block">
      1 of 3
    </div>
    <div class="col-md-8 col-sm-10 offset-sm-1 offset-md-0">
      2 of 3 (wider)
    </div>
    <div class="col d-sm-none d-md-block">
      3 of 3
    </div>
  </div>
</div>
```

*http://getbootstrap.com/docs/4.0/layout/grid/#offsetting-columns*

---

## Horizontal alignment

![](https://i.imgur.com/6OyXrwh.png)

*http://getbootstrap.com/docs/4.0/layout/grid/#horizontal-alignment*

----

```htmlmixed=
<div class="container">
  <div class="row justify-content-start">
    <!-- 2 div .col-4 -->
  </div>
  <div class="row justify-content-center">
    <!-- 2 div .col-4 -->
  </div>
  <div class="row justify-content-end">
    <!-- 2 div .col-4 -->
  </div>
  <div class="row justify-content-around">
    <!-- 2 div .col-4 -->
  </div>
  <div class="row justify-content-between">
    <!-- 2 div .col-4 -->
  </div>
</div>
```

---

## Vertical alignment

![grid layout](https://i.imgur.com/yd18sBg.png)

*http://getbootstrap.com/docs/4.0/layout/grid/#vertical-alignment*

----

```htmlmixed=
<div class="container">
  <div class="row align-items-start">
    <!-- 3 div .col -->
  </div>
  <div class="row align-items-center">
    <!-- 3 div .col -->
  </div>
  <div class="row align-items-end">
    <!-- 3 div .col -->
  </div>
</div>
```

---

## Advanced usage

<b>With sass it is easy to reuse bootstrap css in our own stylesheet</b>

* Variables
* Functions (mixins)

---

### Change bootstrap's behavior

* Responsive breakpoints
* Number of columns
* Gutter width
* Container max width
* Colors

*http://getbootstrap.com/docs/4.0/layout/grid/#variables*

----

```sass
$grid-columns:      12;
$grid-gutter-width: 30px;

```

----

```sass
$grid-breakpoints: (
  // Extra small screen / phone
  xs: 0,
  // Small screen / phone
  sm: 576px,
  // Medium screen / tablet
  md: 768px,
  // Large screen / desktop
  lg: 992px,
  // Extra large screen / wide desktop
  xl: 1200px
);


```

----

```sass
$container-max-widths: (
  sm: 540px,
  md: 720px,
  lg: 960px,
  xl: 1140px
);

```

---

### Custom css classes

Make your custom classes using `bootstrap-sass` functions (`mixins`).

*http://getbootstrap.com/docs/4.0/layout/grid/#mixins*

----

```sass=
.example-content-main {
  @include make-col-ready();

  @include media-breakpoint-up(sm) {
    @include make-col(6);
  }
  @include media-breakpoint-up(lg) {
    @include make-col(8);
  }
}
```

----

```htmlmixed=
<div class="example-content-main">
    <!-- content here -->
</div>
```

is the same as:

```htmlmixed=
<div class="container"> <!-- .container set a width -->
    <div class="col-sm-6 col-lg-8">
        <!-- content here -->
    </div>  
</div>
```

---

## Utilities

Almost all CSS features are wrapped into bootstrap.

*https://getbootstrap.com/docs/4.0/utilities*

They provide:
* Mostly CSS classes
* Some SASS variables
* Some SASS mixins

---

## Bootstrap JS

* PopperJS and JQuery
* Mainly for components
* Per component documentation

---

# Conclusion

* the wheel is not reinvented
* save time
* allows to have a workflow which would be difficult to set up manually
* bootstrap impose itself as a standard for grid system

---