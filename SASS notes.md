//Let's begin with some notes on SCSS for reinforcement

# Before

```scss
.home{
 .intro-section.section{
  padding-bottom: 8em;
  padding-top:2em;
  color:#F0D6B5;
  }
}

 .intro-section.section{
  .intro{
    padding-top: 75px;
    max-width: 1000px;
    margin: 0 auto;
  }
  h1{
    font-family:'DiplomaScript';
    font-weight: 400;
    font-size:5em;
    padding-top: 1em;
    overflow: hidden;
    text-align: center;
    }
  h1.centerlines{
    color:#F0D6B5;
  }
}
```

# after

```scss
.home{
  //.home
 .intro-section.section{
  //.home .intro-section.section
  padding-bottom: 8em;
  padding-top:2em;
  color:#F0D6B5;
  .intro{
    //.home .intro-section.section .intro
    padding-top: 75px;
    max-width: 1000px;
    margin: 0 auto;
  }
  h1{
    //.home .intro-section.section h1
    font-family:'DiplomaScript';
    font-weight: 400;
    font-size:5em;
    padding-top: 1em;
    overflow: hidden;
    text-align: center;
    &.centerlines{
    //.home .intro-section.section h1.centerlines
    color:#F0D6B5;
  }
}
```


# Examination of Ampersands

## No Ampersand

```scss
h1 {
  .centerlines {
    //...
  }
}
```

Compiles to:
```css
h1 .centerlines {
  //...
}
```

Will target: h1 .centerlines
```html
<h1>
  <span class="centerlines">I have a centerline!</span>
</h1>
```

(Note element inside h1 does not have to be a span! It also does not need to be the first direct "child" of h1.)

Can also target:
```html
<h1>
  <span>
    <span>
      <span class="centerlines">I have a centerline!</span>
    </span>
  </span>
</h1>
```

## With Ampersand

```scss
h1 {
  &.centerlines {
    //...
  }
}
```

Compiles to:

```css
h1.centerlines {
  //...
}
```

Will target:

`h1.centerlines`

```html
<h1 class="centerlines">I have a centerline!</h1>
```

## Another use case with ampersands

```scss
h1 {
  &:hover {
    //...
  }
}
```

Compiles to:

```css
h1:hover {
  //...
}
```

Remember:
  If there is NO SPACE between two selectors then you are targeting the element's class. Ex:
  h1.centerlines targets the header1 elements class which is "centerlines".
  When there IS A SPACE between two selectors then you are targeting the object housed within the first element. Ex:
  "h1 .centerlines" targets the "centerlines" element housed within h1.

//CHANGES TO MY PERSONAL SITE FROM CSS TO SCSS:

---
# Only the main Sass file needs front matter (the dashes are enough)
---
@charset "utf-8";

@font-face {
    font-family:'NimbusSan';
    src: url('../NimbusSan-Reg.woff');
    font-weight: 400;
}
@font-face {
    font-family:'NimbusSan';
    src: url('../NimbusSan-Bol.woff');
    font-weight:700;
}

@font-face {
    font-family:'NimbusSan';
    src: url('../NimbusSan-RegIta.woff');
    font-weight:400;
    font-style: italic;
}
@font-face {
    font-family:'NimbusSan';
    src: url('../NimbusSan-BolIta.woff');
    font-weight:700;
    font-style: italic;
}
@font-face {
    font-family:'DiplomaScript';
    src: url('../DiplomaScript-Basic.woff');
    font-weight:400;
}

@font-face {
    font-family:'NimbusSan';
    src: url('../NimbusSanExt-Lig.woff');
    font-weight:100;
}

// Our variables
$base-font-family: "Helvetica Neue", Helvetica, Arial, sans-serif;
$base-font-size:   16px;
$base-font-weight: 400;
$small-font-size:  $base-font-size * 0.875;
$base-line-height: 1.5;

$spacing-unit:     30px;

$text-color:       #fefefe;
$background-color: #111111;
$brand-color:      #A48051;

$black:            #111111;

$grey-color:       #828282;
$grey-color-light: lighten($grey-color, 40%);
$grey-color-dark:  darken($grey-color, 25%);



// Width of the content area
$content-width:    800px;

$on-palm:          600px;
$on-laptop:        800px;



// Use media queries like this:
// @include media-query($on-palm) {
//     .wrapper {
//         padding-right: $spacing-unit / 2;
//         padding-left: $spacing-unit / 2;
//     }
// }
@mixin media-query($device) {
    @media screen and (max-width: $device) {
        @content;
    }
}



// Import partials from `sass_dir` (defaults to `_sass`)
@import
        "base",
        "layout",
        "syntax-highlighting"
;

body {
  //background-color: $black !important;
  background-color: #111111 !important;
  color: white;
}

body p{
  color: #F0D6B5;
}

h1.post-title{
  color: #167AA1;
  margin-bottom: 25px;
  margin-top: 25px;
}

.home {
  .section {
    background-color: $black;
    color: $text-color;
  }
  h1 {
    color: $brand-color;
    text-align: center;
  }
}
.home {
  .banner-section {
    h1 {
      text-align: center;
      font-size:10em;
      margin-bottom: 0;
      padding: 200px 0;
      .beauty {
font-family:'NimbusSan';
font-weight:60;
color:#F5EDD9;
      }
      .utility {
font-family:'NimbusSan';
font-weight: 700;
color:#F5EDD9;
      }
      .elegance {
font-family:'DiplomaScript';
font-size: 1.5em;
display: block;
padding-top:.5em;
color:$brand-color;
      }
    }
  }
}

.home{
 .intro-section.section{
  padding-bottom: 8em;
  padding-top:2em;
  color:#F0D6B5;
    .intro{
    padding-top: 75px;
    max-width: 1000px;
    margin: 0 auto;
  }
    h1{
    font-family:'DiplomaScript';
    font-weight: 400;
    font-size:5em;
    padding-top: 1em;
    overflow: hidden;
    text-align: center;
    }
    &.centerlines{
    color:#F0D6B5;
  }
}

/*HEADER LINES*/

h1{
&.centerlines{
overflow: hidden;
text-align: center;}
  :before,
  :after {
 background-color: $brand-color;
 content: "";
 display: inline-block;
 height: 1px;
 position: relative;
 vertical-align: middle;
 width: 50%;}
  :before {
 right: 0.5em;
 margin-left: -50%;}
  :after {
 left: 0.5em;
 margin-right: -50%;}
            }
          }
        }
      }
    }
  }
