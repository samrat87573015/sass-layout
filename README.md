___

## Sass Installation

````scss
npm install -g sass 

// Compiled
sass style.scss style.css

//auto Compiled
sass --watch  assets/scss/style.scss assets/css/style.css

````

___

## Sass Variables

**Typed Variables:**  Define variables with specific types, such as numbers, strings, colors, or lists.

```scss
$primary-color: #FF6347; // Color
$font-size: 16px; // Number
$font-stack: "Arial", sans-serif; //
String $font-size-responsive: (sm: 16px, md: 26px, lg: 36px); // Map
```

___

**Usage:** Utilize typed variables just like regular ones, ensuring consistency and type safety throughout your stylesheets.

```scss
// Sass Variables with Types
// Sass Variables with Types

$primary-color: #FF6347; // Color 
$font-size: 16px; // Number

$font-stack: "Arial", sans-serif; // String 
$font-size-responsive: (sm: 16px, md: 26px, lg: 36px); // Map 
// Example Usage 
.button { background-color: $primary-color; font-size: $font-size; font-family: $font-stack; } 
// Responsive Font Size Usage 
@media screen and (min-width: 576px) { 
	.button { 
		font-size: map-get($font-size-responsive, sm); 
	} 
} 
@media screen and (min-width: 768px) { 
	.button { 
		font-size: map-get($font-size-responsive, md); 
	} 
} 
@media screen and (min-width: 992px) { 
	.button { 
		font-size: map-get($font-size-responsive, lg);
	} 
}

```

___

### Sass Nesting

```html
    <nav>
        <ul>
	        <li><a href="#">Home</a></li>
	        <li><a href="#">About</a></li>
	        <li><a href="#">Services</a></li>
	        <li><a href="#">Contact</a></li>
        </ul>

    </nav>

```

```scss
// Define styles for the navigation bar

nav {

    background-color: #333;

    padding: 10px;
    // Style the unordered list inside the navigation bar

    ul {

        list-style: none;

        margin: 0;

        padding: 0;

        // Style list items

        li {

            display: inline-block;

            margin-right: 10px;

            // Style links inside list items

            a {

                color: #fff;

                text-decoration: none;

                padding: 5px 10px;

                // Change link color on hover

                &:hover {

                    background-color: #555;

                }

            }
	    }
    }
}
```

___

### Sass @import and Partials

1. **Create Partial Files:** Name your partial Sass files with a leading underscore, like ` _variables.scss , _mixins.scss `, etc. This convention tells Sass not to compile them into separate CSS files.
2. **Define Styles:** Write your CSS rules or Sass variables, mixins, or functions inside these partial files.

```scss
@import 'variables';

```

___

## Sass `Mixins`


Sass `mixins` allow you to define reusable sets of CSS declarations that can be included anywhere in your stylesheets

**Define Mixins:** Use the @mixin directive followed by a name and a set of CSS declarations within curly braces.

```scss
@mixin button-styles { 
	border: 1px solid #ccc;
	padding: 10px 20px; 
	background-color: #f0f0f0; 
	color: #333; 
} 

.button { 
	@include button-styles; 
}

```

___

### Sass @extend and Inheritance

The `@extend` directive in Sass allows you to share a set of CSS properties from one selector to another, effectively inheriting styles.

```scss
// Define a base button style

.btn-base {
    border: 1px solid #ccc;
    padding: 10px 20px;
    background-color: #f0f0f0;
    color: #333;
}

// Apply the base style to specific buttons

.btn-primary {
    @extend .btn-base;
    background-color: #FF6347; // Customize specific properties for primary button
}

.btn-secondary {
    @extend .btn-base;
    background-color: #6495ED; // Customize specific properties for secondary button
}
```

___

### Control Directives `@if @else`

The `@if` and `@else` directives in Sass provide conditional logic for applying styles based on specified conditions

```scss
$use-dark-theme: true;

.navbar {

    @if $use-dark-theme {
        background-color: #333;
        color: #fff;
    }
    
    @else {
        background-color: #fff;
        color: #333;
    }

}
```

___

### Control Directives `@for`

The `@for` directive in Sass allows you to loop over a range of values and generate styles accordingly

```scss

@for $i from 1 through 3 {
    .item-#{$i} {
        width: 100px * $i;
    }
}
```

___

### Control Directives `@each`

#### Color


The `@each` directive in Sass allows you to loop over each item in a list or map and apply styles accordingly

```scss

$colors: (
    common: (
        white: #ffffff,
        black: #000,
        black-2: #24292d,
    ),
    heading: (
        primary: #343a40,
    ),
    grey: (
        1:#c5c5c5,
        2: #aeaeae,
        3: #acacac,
        4: #999999,
        5: #f7f7f7,
        6: #b7b7b7,
        7: #a6aeb5,
        8: #edf2f6,
    ),
    text: (
        body:#777777,
        1:#000,
    ),
    theme: (
        1: #20de59,
        2: #fff1f1,
    ),
    border: (
        1: #ededed,
        2: #e9e9e9,
        3: #999999,
    )

);

:root {
    /**
    @color declaration
    */
    @each $color, $shades in $colors {
        @each $shade, $value in $shades {
            --tp-#{$color}-#{$shade}: #{$value};
        }
    }
}

```

#### Css result

```css

:root {
  /**
  @color declaration
  */
  --tp-common-white: #ffffff;
  --tp-common-black: #000;
  --tp-common-black-2: #24292d;
  --tp-heading-primary: #343a40;
  --tp-grey-1: #c5c5c5;
  --tp-grey-2: #aeaeae;
  --tp-grey-3: #acacac;
  --tp-grey-4: #999999;
  --tp-grey-5: #f7f7f7;
  --tp-grey-6: #b7b7b7;
  --tp-grey-7: #a6aeb5;
  --tp-grey-8: #edf2f6;
  --tp-text-body: #777777;
  --tp-text-1: #000;
  --tp-theme-1: #20de59;
  --tp-theme-2: #fff1f1;
  --tp-border-1: #ededed;
  --tp-border-2: #e9e9e9;
  --tp-border-3: #999999;
}

```

___

### Responsive Breakpoint


```scss

// Responsive Variables
$xxxl: 'only screen and (min-width: 1601px) and (max-width: 1700px)';
$xxl: 'only screen and (min-width: 1400px) and (max-width: 1600px)';
$xl: 'only screen and (min-width: 1200px) and (max-width: 1399px)';
$lg : 'only screen and (min-width: 992px) and (max-width: 1199px)';
$md:'only screen and (min-width: 768px) and (max-width: 991px)';
$sm: 'only screen and (min-width: 576px) and (max-width: 767px)';
$xs:'(max-width: 575px)';


.title {
    color: var(--tp-theme-1);
    background: #000;
    display: block;
    padding: 10px 20px;
    margin-top: 200px;
    
    @media #{$md,$sm,$xs} {
        background: var(--tp-grey-2);
    }

}

```


