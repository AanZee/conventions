# CSS and CSS Preprocessors

The goals of these conventions are to create reusable style sheets and to keep them maintainable, transparent, readable, and scalable. Although SCSS and CSS is used for the examples, it does not matter if you use Less, SCSS, or even plain CSS. Choose a language based on the nature of your project. Each language has its own strengths.

For these conventions a [CSScomb config file is available](attachments/.csscomb.json).

## Table of Contents
- [Terminology](#terminology)
- [Grouping and Ordering](#grouping-and-ordering)
- [Code spacing](#code-spacing)
- [Naming](#naming)
- [Selectors](#selectors)
- [Nesting](#nesting)
- [Declarations](#declarations)
- [Values](#values)
- [Comments](#comments)
- [Performance](#performance)
- [Specific Techniques](#specific-techniques)

## Terminology

This document assumes you are familiar with the terminology for CSS and CSS preprocessors. A short refresher:

- **Rule** = combination of selector group and declaration block.
- **Selector group** = All the selectors within a rule. Selectors within a selector group are separated by a comma.
- **Selector** = Pointer to an element in your HTML page.
- **Simple selector** = Part of a selector. Simple selectors within a selector are separated by a combinator.
- **Combinator** = Describes the relation between simple selectors.
- **Property** = Aspect of the selector you are styling.
- **Value** = Setting of the property.
- **Declaration** = Combination of a property and its value.
- **Declaration block** = All the declarations within a rule.

**Rule:**
```CSS
selector,
simple-selector > simple-selector {
	property: value;
	property: value;
	property: value;
}
```

## Grouping and Ordering

### Rules should be ordered based on specificity

- If you use Less or SCSS, you should divide your code across multiple files and organize it in different directories. The groups and order can be found in the list below.
- With Less or SCSS, never divide a rule group (e.g. BEM block) across different files.
- With Less or SCSS, never combine different rule groups (e.g. BEM blocks) in one file.
- Never use sub-folders to group files.
- With Less or SCSS, each group should have an index file (e.g. '\_index.scss') which includes all the files from that directory. Only the indexes should be included in the main SCSS or Less file.
- Rules within vendors, utilities, or layout are [immutable](http://csswizardry.com/2015/03/immutable-css/).

**Order should be:**

1. **vendors** (e.g. Bourbon, Bootstrap, jQuery UI)
2. **fonts** (font-facing)
3. **settings** (variables and configs, e.g. colors, fonts families, font sizes, line heights, animations variables)
4. **utilities** (e.g. your mixins, functions, and tools)
5. **vendor-overrides** (to re-declare some vendor CSS with help of settings and utilities, if needed)
6. **reset** (e.g. [Reset CSS](http://meyerweb.com/eric/tools/css/reset/) or [normalize.css](http://necolas.github.io/normalize.css/), and [box-sizing](http://www.paulirish.com/2012/box-sizing-border-box-ftw/))
7. **layout** (immutable objects, e.g. grid, body with a sticky footer, views)
8. **controls** (e.g. buttons, segmented-control, drop-down-menu, pop-up-menu, text-inputs)
9. **components** (designed interface blocks: bars, dialogs, indicators, content)
10. **pages** (page specific styles. Before you add page specific styles, consider modified components. Also note that components that can only be found on one page but still could be used on other pages should be placed in 'components')
11. **themes** (for many projects non-existent)
12. **overrides** (hacks and things you are not proud of)

See [The Specificity Graph](http://csswizardry.com/2014/10/the-specificity-graph/) and [CSS Specificity Graph Generator](http://jonassebastianohlsson.com/specificity-graph/) for more information about CSS specificity.

**File names should be:**

1. **vendors**: original directories and file names.
2. **fonts**: name of typeface.
3. **settings**: name of property or use.
4. **utilities**: name of function or mixin.
5. **vendor-overrides**: same as vendor's directories or file names.
6. **reset**: original file name or function name.
7. **layout**: name of container or function.
8. **controls**: name of control.
9. **components**: name of block.
10. **pages**: name of page or template.
11. **themes**: name of theme.
12. **overrides**: depends on type.

### Do not use @import for CSS files

- Importing CSS files has a negative impact on performance.
- Create a link to the CSS file in the HTML head instead, or better: download the CSS file, place it in the correct group and change the CSS extension to the extension of your preprocessor. This forces the compiler to add the rules into your own CSS file.

### Properties should be ordered based on functionality

- Increases readability, understanding, and the ability to find duplicate properties.
- SCSS or Less includes should be placed first, before all declarations within a rule. This is to improve readability and to assure declarations from includes cannot override specific declarations.

**Order should be:**

1. Positioning
2. Box behavior and properties
3. Sizing
4. Color appearance
5. Special content types
6. Text
7. Visual properties
8. Print

Tools like [CSScomb](http://csscomb.com), in combination with [a CSScomb config file](attachments/.csscomb.json) based on these conventions, can be used to automate ordering.

### Place rules in media queries, unless applicable for all media queries

Only rules applicable to all media queries should be placed outside a media query. All other rules should be written per media query. This makes sure you never have to overwrite rules in an other media query, the code is easier to read, and it [improves render performance](http://meiert.com/en/blog/20080419/reset-style-sheets-are-bad/). This means that you should not write CSS rules mobile first and change the rules for bigger viewports. You write CSS rules meant for a viewport only for that specific viewport. This doesn't mean you shouldn't design mobile first.

**Right:**
```CSS
.class {
	background-color: red;
}

@media screen and (max-width: 440px) {
    .class {
        padding: 20px;
    }
}

@media screen and (min-width: 441px) and (max-width: 1040px) {
    .class {
        padding: 40px;
    }
}

@media screen and (min-width: 1041px) {
    .class {
        padding: 60px;
    }
}
```

**Wrong:**
```CSS
.class {
	background-color: red;
	padding: 20px;
}

@media screen and (min-width: 441px) {
    .class {
        padding: 40px;
    }
}

@media screen and (min-width: 1041px) {
    .class {
        padding: 60px;
    }
}
```

## Code Spacing

### Rules should be separated by one empty line

**Right:**
```CSS
selector {
	property: value;
}

selector {
	property: value;
}
```

**Wrong:**
```CSS
selector {
	property: value;
}
selector {
	property: value;
}


selector {
	property: value;
}
```

### Selectors, separated by a comma, should be placed on separate lines

- Makes it easier to find and optimize selectors.

**Right:**
```CSS
selector,
simple-selector simple-selector,
selector {
	property: value;
}
```

**Wrong:**
```CSS
selector, simple-selector simple-selector, selector {
	property: value;
}
```

### Declarations should be on a separate line

**Right:**
```CSS
selector {
	property: value;
	property: value;
	property: value;
}
```

**Wrong:**
```CSS
selector {
	property: value; property: value;

	property: value;
}
```

#### Exception
In case of many selectors with similar properties it is allowed to place selectors and declarations on a single line.

**Right:**
```CSS
.selector--m1 { background-color: red; }
.selector--m2 { background-color: blue; }
.selector--m3 { background-color: yellow; }
```

**Wrong:**
```CSS
.selector--m1 { font-size: 12px; background-color: red; }
.selector--m2 { color: white; background-color: blue; }
.selector--m3 { opacity: 0.5; background-color: yellow; }
```

### Strings should be quoted with a single quote

**Right:**
```CSS
selector {
	font-family: 'Helvetica Neue Light', 'Helvetica', 'Arial', sans-serif;
	background-image: url('/images/image.jpg');
}
```

**Wrong:**
```CSS
selector {
	font-family: "Helvetica Neue Light", "Helvetica", "Arial", sans-serif;
	font-family: Helvetica Neue Light, Helvetica, Arial, sans-serif;
	background-image: url(/images/image.jpg);
}
```

### Value lists should be written on the same line

- Exception: only very long comma separated values, such as font-face URLs and gradients, may be written on different lines to improve readability.

**Right:**
```CSS
@font-face {
	font-family: 'Source Sans Pro';
	font-weight: 400;
	font-style: normal;
	src: url('../fonts/SourceSansPro/SourceSansPro-Regular.eot');
	src: url('../fonts/SourceSansPro/SourceSansPro-Regular.eot?#iefix') format('embedded-opentype'),
		url('../fonts/SourceSansPro/SourceSansPro-Regular.woff2') format('woff2'),
		url('../fonts/SourceSansPro/SourceSansPro-Regular.woff') format('woff'),
		url('../fonts/SourceSansPro/SourceSansPro-Regular.ttf') format('truetype');
}

selector {
	font-family: 'Source Sans Pro', 'Helvetica', 'Arial', sans-serif;
}
```

**Wrong:**
```CSS
selector {
	font-family:
		'Helvetica Neue Light',
		'Helvetica',
		'Arial',
		sans-serif;
}
```

### Other spacing conventions

- Add spaces before and after a selector combinator (e.g. ' > ').
- Remove spaces before selector delimiter (',').
- Add a space between selector and opening brace ('{').
- Add a line break after the opening brace ('{').
- No spaces between property and colon (':').
- Add a space between colon (':') and value.
- Comma-separated values should include a space after each comma.
- Parentheses ('()') should not be padded with spaces.
- Align prefixes.
- Add a trailing semi-colon (';') after the last declaration.
- Add a line break before closing brace ('}').
- Trim trailing spaces or tabs.
- Add an empty line at end of file.

Tools like [CSScomb](http://csscomb.com), in combination with [a CSScomb config file](attachments/.csscomb.json) based on these conventions, can be used to automate spacing.

## Naming

### Write selectors in lower-case and use hyphen-delimited syntax

- CSS is a hyphen-delimited syntax.
- Makes it easier to read and scan.

**Right:**
```CSS
selector-name {}
```

**Wrong:**
```CSS
SelectorName {}
SELECTOR_NAME {}
```

See ['CSS: CamelCase Seriously Sucks!'](http://csswizardry.com/2010/12/css-camel-case-seriously-sucks/) for further reading.

### Selector names should follow 'BEM Methodology' honed by Nicolas Gallagher

- Enables you to write modular based CSS, which makes it easier to manage larger projects that last a while.
- BEM is an acronym for Block, Element and Modifier.
- Blocks are independent and can be used in different situations.
- The name of a block should be well thought out. Take your time. Always use UI dictionaries or Human Interface Guidelines from Apple, Google or Microsoft as reference for a semantically correct name.
- The name of an element, a part of a block, is a combination of the surrounding block and the element, divided with two underscores '\_\_'.
- The name of a modified block or modified element is a combination between the complete name and the modifier, divided with two hyphens '--'.
- Modification means a different version of a block or element.
- Modifiers are timeless. Use 'states' if a 'different version' is temporarily.
- A block can be nested within an element from another block if that block is often used by itself.
- A class does not reflect the full trail of the DOM. Only one block or element is allowed within a class name.
- A modified block or element still inherits a lot of styling from the original block or element. A new block or element is completely independent from the original block or element. You determine the tipping point, but if in doubt create a new block or element.
- Don't create unnecessary blocks, make sure a block has a clear purpose and can be used in different situations. If this is not the case, keep it as an element within its block.
- Never set a margin on a block. A block does not determine the space around itself. This is done by the parent element from the parent block.
- It is not allowed to give a block or element two BEM classes.
- It is not allowed to place an element class from a block in another block.

**Right:**
```CSS
.block {}
.block__element {}
.block--modifier {}
.site-search {} /* Block */
.site-search__field {} /* Element */
.site-search--full {} /* Modifier */
.person {}
.person__hand {}
.person--female {}
.person--female__hand {}
.person__hand--left {}
.person {}
.hand {}
.female {}
.female-hand {}
.left-hand {}
```

**Wrong:**
```CSS
.block__element__element {}
.block__block__element {}
```

See [BEM](https://bem.info), [CSS Wizardry](http://csswizardry.com/2013/01/mindbemding-getting-your-head-round-bem-syntax/), [Google's Web Fundamentals](https://developers.google.com/web/fundamentals/performance/rendering/reduce-the-scope-and-complexity-of-style-calculations#use-block-element-modifier), and [Side Effects in CSS](http://philipwalton.com/articles/side-effects-in-css/) for further reading.

### Never style HTML elements directly, always use class names.

- Also applies to typographic elements such as 'h1' and 'p'. For user content or other content containing only HTML elements without class names, use the class '.content' as a container. The 'content block' should be placed in the components folder.
- Exception applies to rules in reset folder.

**Right:**
```CSS
.content h1 {}
.content p {}
.content ul {}
```

**Wrong:**
```CSS
h1 {}
p {}
ul {}
```

See [Modular CSS typography](http://thesassway.com/advanced/modular-css-typography) and [Side Effects in CSS](http://philipwalton.com/articles/side-effects-in-css/) for further reading.

### Descriptive size names

#### Max widths
Large to small:

```text
- expanded
- extended
- wide
- default
- narrow
- condensed
- compressed
```

#### Resize
```text
- stretched (stretches to the size of it's parent)
- fitting (resize to fit it's children)
```

### Names of variants (within a rhythm) for selectors or variables should follow 'city block sizes'

- The standard variant of a pattern gets the modifier '100'.
- There are two standard variants: with and without a number. Especially useful when you start patterns without variants and you have to add variants later on in a project. You don't want to change all the names in your project.
- Smaller variants get the modifiers '90', '80', '70',…
- Larger variants get the modifiers '200', '300',…
- A modifier that removes paddings or height from a block can be written as '0', for example pane--0 is a section without padding-top and padding-bottom.
- Numbers don't resemble exact size ratios, because that would be descriptive naming: button--200 is not necessary twice as large as button--100.
- City block sizes for Less or SCSS variables should be written as part of the name (right: '$line-height-200') and should not be written as BEM modifiers (wrong: '$line-height--200').

**Right:**
```SCSS

.button {
	property: value;
}

.button--90 {
	property: value;
}

.button--100 {
	.button;
}

.button--200 {
	property: value;
}
```

**Wrong:**
```SCSS
.button--small {
	property: value;
}

.button--medium {
	property: value;
}

.button--large {
	property: value;
}
```

See ['How to build the perfect pattern library'](http://www.slideshare.net/WolfBruening/how-to-build-the-perfect-pattern-libraryy) for further reading.

### Fractions used for grids and modifiers should be spelled out in full

City block sizes are used for rhythms, never for exact values or fractions. When you want to specify that an object should be exactly one third or two tenths of a width, add modifiers as: .class--one-third or .class--two-tenths. When you want to create a modifier for full width, use: .class--full.

**Right:**
```CSS
.column--one-third {}
.column--two-tenths {}
.column--full {}
```

**Wrong:**
```CSS
.column--1-3 {}
.column--2-10 {}
.column--1 {}

.column--80 {}
.column--90 {}
.column--100 {}
```

### Range specific modifiers should end with specified suffix

Range specific modifiers should end with 'range-and-larger' or 'range-and-smaller'.

**Right:**
```CSS
.component--modifier-lap-and-larger {}
.component--modifier-desk-l-and-larger {}

.component--modifier-hand-and-smaller {}
.component--modifier-lap-m-and-smaller {}
```

**Wrong:**
```CSS
.component--modifier-lap-and-higher {}
.component--modifier-desk-l-and-more {}
.component--modifier-desk-l-and-up {}

.component--modifier-hand-and-less {}
.component--modifier-lap-m-and-under {}
.component--modifier-lap-m-and-lower {}
```

### Modifiers for different flex-grows should be written out in full

Depending on the 'grow value' (default is 1) and the amount of elements within a flex container, an element takes more or less space within the flex container. Flex-grow doesn't dictate a fixed size or fraction, it is a unit-less value. For more about flex-grow and Flexbox Layout see ['A Complete Guide to Flexbox'](https://css-tricks.com/snippets/css/a-guide-to-flexbox/). These unit-less values should be written out in full.

**Right:**
```CSS
.class--takes-two {
	flex-grow: 2;
}

.class--takes-three {
	flex-grow: 3;
}
```

**Wrong:**
```CSS
.class--2 {
	flex-grow: 2;
}

.class--3 {
	flex-grow: 3;
}
```

### Names of variables should start with the property or type

- Makes it easier to group them and to use autocomplete in development tools.

**Right:**
```SCSS
$font-family-monospace: ;
$color-blue: ;
```

**Wrong:**
```SCSS
$monospace-font-family: ;
$blue-color: ;
```

### Names of variables for colors should be written both descriptive and functional

- Start with descriptive variables, followed by the functional variables.
- City block sizes may be used for functional names. Higher number means darker, lower number means lighter. You can use Less or SCSS functions to control the variants. It is also possible to use descriptive names for variants.
- Use variables even for black or white, because black and white could contain, depending on the style guide, a subtle tint.
- Good functional colors are: color-ui; color-ui-accent; color-heading; color-subheading; color-text; color-text-diap; color-cta; color-primary; color-secondary; color-tertiary; color-error; color-success; color-select; color-focus;

**Right:**
```SCSS
// Descriptive colors

$color-silver: #323232;

// Functional colors

$color-primary: $color-silver;
$color-primary-90: lighten($color-primary-100, 10%)
$color-primary-100: $color-primary;
$color-primary-200: darken($color-primary-100, 10%)
```

**Wrong:**
```SCSS
$color-primary: #323232;
```

See ['Name that Color'](http://chir.ag/projects/name-that-color/) for example for finding descriptive names.

### Local variables should start with the name of the block and end with a property

- Local variables are written directly above the block rule in the same file.
- Local variables may only be used in the block it is created for. Local variables written above the block rule are technically not local in SCSS or Less and can be used everywhere. You should never do this.
- Local variables should function as 'settings' for a block.
- For local variables, combine name of the block and, in some cases, the element with the property. Only use hyphens as delimiters. Do not use the BEM notation for variables.
- Make as few settings as possible, and try to use block settings for elements. For example border colors are not always set on a block but on different elements within a block. If the border color should be the same for all these elements, create only one block variable.
- Use local variables mostly for colors.
- Use global functional colors, not descriptive colors, to set local variables.
- Within SCSS, local variables are set as default variables with '!default'.

Example written for SCSS:

**Right:**
```SCSS
$button-background-color: $color-secondary !default;
$button-border-color: $color-secondary-200 !default;
```

**Wrong:**
```SCSS
$button-background-color: $color-red !default;
$border-color-button: $color-secondary-200;
```

### Names of media queries should be based on the context of a device

- There are major and minor ranges.
- Major ranges should be based on the context of a device.
- Minor ranges (a.k.a. tweak points) are based on size differences within major ranges.
- Breakpoints should only be used if the content requires it.
- Use 'media' mixin for setting ranges.
- Use '0' and 'false' in the media mixin to set the outer ranges.

**Visual presentation of ranges:**
```
|--palm--|--hand--|--lap--|--desk--|
```

**Right:**
```SCSS
$range-palm   : ( 320,  440);
$range-palm-s : ( 320,  360);
$range-palm-m : ( 361,  400);
$range-palm-l : ( 401,  440);

$range-hand   : ( 441,  680);
$range-hand-s : ( 441,  520);
$range-hand-m : ( 521,  600);
$range-hand-l : ( 601,  680);

$range-lap    : ( 681, 1040);
$range-lap-s  : ( 681,  800);
$range-lap-m  : ( 801,  920);
$range-lap-l  : ( 921, 1040);

$range-desk   : (1041, false);
$range-desk-s : (1041, 1280);
$range-desk-m : (1281, 1640);
$range-desk-l : (1641, 2560);

.selector {

	@include media(0, $range-palm) {
		property: value;
	}

	@include media($range-hand, $range-lap) {
		property: value;
	}

	@include media($range-desk, false) {
		property: value;
	}

}
```

**Wrong:**
```SCSS
$breakpoint-small:   440px;
$breakpoint-smedium: 680px;
$breakpoint-medium:  920px;
$breakpoint-large:   1040px;
```

See ['Responsive grid systems; a solution?'](http://csswizardry.com/2013/02/responsive-grid-systems-a-solution/) and ['Tweakpoints'](http://adactio.com/journal/6044/) for further reading.

## Selectors

### Name selectors with reusability in mind

- The name of a block or element should be well thought out. Take your time. Always use UI dictionaries or Human Interface Guidelines from Apple, Google or Microsoft as reference for a semantically correct name.
- Ask yourself if you could use the selector name multiple times in your project as well as other projects.

**Right:**
```CSS
.menu__item {}
.is-highlighted {}
.sheet {}
```

**Wrong:**
```CSS
.menu-item-about-us {}
.red {}
.border-top {}
.border-right {}
```

### Never reference IDs from CSS files

- IDs are overly specific and unnecessary.
- Performance difference between classes and IDs is irrelevant.

**Right:**
```CSS
.class {
	property: value;
}
```

**Wrong:**
```CSS
#id {
	property: value;
}
```

See['Don't use IDs in CSS selectors?'](http://oli.jp/2011/ids/) for further reading.

### Never reference class names in your CSS files used by other applications or languages

- Never reference, for example, classes prefixed with 'js-', 'test-', or 'track-', which are used by Javascript, testing, or tracking tools.

### Use states as separate classes and add them to existing selectors

- States differ from modifiers. Modifiers are timeless, states are temporarily.
- States never contain global styling. Style states always in combination with other selectors. This makes it easier to reuse components in different projects.
- States are allowed to be nested with Less or SCSS. Usage is similar to pseudo-classes and pseudo-elements.
- States always start with 'is'.

**Right:**
```SCSS
.selector {

	&.is-visible {
		property: value;
	}

	&.is-hidden {
		property: value;
	}

	&.is-added {
		property: value;
	}

	&.is-removed {
		property: value;
	}

	&.is-active {
		property: value;
	}

	&.is-disabled {
		property: value;
	}

	&.is-collapsed {
		property: value;
	}

	&.is-expanded {
		property: value;
	}

	&.is-highlighted {
		property: value;
	}

	&.is-invalid {
		property: value;
	}

	&.is-valid {
		property: value;
	}

	&.is-dragging {
		property: value;
	}

	&.is-dropped {
		property: value;
	}

	&.is-selected {
		property: value;
	}

	&.is-filled {
		property: value;
	}

	&.is-empty {
		property: value;
	}

	&.is-updating {
		property: value;
	}

	&.is-loaded {
		property: value;
	}

	&.is-loading {
		property: value;
	}

}
```

**Wrong:**
```SCSS
.is-hidden {
	display: none;
}

.hidden {
	display: none;
}
```

### Use CSS3 syntax for pseudo-elements

- Use two colons for pseudo-elements and one colon for pseudo-classes. Pseudo-elements are new virtual elements created by CSS, such as 'before' and 'after'. These elements do not exist otherwise. Pseudo-classes select existing elements that cannot be selected using other simple selectors. Examples are 'first-child', 'last-child', and 'hover'.

**Right:**
```SCSS
selector

	&::before {
		property: value;
	}

}
```

**Wrong:**
```CSS
selector {

	&:before {
		property: value;
	}

}
```

## Nesting

### A selector may contain no more than three simple selectors

- Even when using the BEM methodology, you cannot avoid cascading. Think about content where you have little control, such as user generated content. In these cases it is allowed to cascade, but never deeper than three levels.

**Right:**
```CSS
.content td p {
	property: value;
}
```

**Wrong:**
```CSS
.content table td p {
	property: value;
}
```

### Do not nest blocks, elements or modifiers with Less or SCSS

- Nesting blocks, elements or modifiers with Less or SCSS makes it more difficult to optimize your CSS.

**Right:**
```CSS
simple-selector-1 {
	property: value;
}

simple-selector-1 simple-selector-2 {
	property: value;
}
```

**Wrong:**
```SCSS
simple-selector-1 {
	property: value;

	& simple-selector-2 {
		property: value;
	}

}
```

### Do nest pseudo-classes, pseudo-elements, media queries, states, and block modifiers for elements with Less or SCSS

- Makes sure style and behavior of the same selector are grouped.
- Also BEM block modifiers (not BEM element modifiers) are nested within BEM elements. This makes it easier for block modifiers to influence different elements and to keep the behavior of an element contained within the Less or SCSS.
- Nested pseudo-classes, pseudo-elements, media queries, states, or BEM block modifiers should also be separated by an empty line.
- The behavior of a pseudo-element should be grouped. Place media queries with rules for a pseudo-element within that pseudo-element. As a result, you don't have to repeat the pseudo-element per media query.
- They way you nest pseudo-elements and pseudo-classes is very different. Pseudo-classes should be nested within media queries when its styling is different per media query. That means you have to repeat pseudo-classes for every media query. The styling of a pseudo-class is related to the styling of the selector per media query. Read [Pseudo-classes vs pseudo-elements](http://www.growingwiththeweb.com/2012/08/pseudo-classes-vs-pseudo-elements.html) to learn more about the difference between pseudo elements and pseudo classes.
- Order media queries based on their ranges.

**Right:**
```SCSS
.selector {
	property: value;

	@include media($range-lap) {
		property: value;

		&:last-child {
			property: value;
		}

	}

	@include media($range-desk) {
		property: value;

		&:last-child {
			property: value;
			property: value;
		}

	}

	&::after {
		property: value;

		@include media($range-lap) {
			property: value;
			property: value;
		}

		@include media($range-desk) {
			property: value;
		}
	}

}
```

## Declarations

### All declarations should end with a semi-colon. Even the last declaration within a rule

- Makes it easier to reorder or add declarations.
- Removing the last semi-colon is needles optimization. Automate this with a compiler or script.

### Avoid shorthand declarations

- It makes it more difficult to overrule a value with a modifier.
- It makes the result of a declaration less predictable and less clear because you often have to set all values, including the values you are not interested in, such as the margins of other sides.

**Right:**
```SCSS
.selector {
	margin-top: 10px;
	background-color: $color-background;
}
```

**Wrong:**
```SCSS
.selector {
	margin: 10px 0 0 0;
	background: $color-background;
}
```

### Use mixins only for prefixes when support is needed

- Use flexbox mixin or other mixins from bourbon or other libraries when you should support browsers which require prefixes.
- Always compare support requirements in the definition of done with browser support via [caniuse.com](http://caniuse.com/) to check if prefixes and mixins are needed.

## Values

### Use variables set in settings as much as possible for values

- Before setting values manually, check variables in settings and use correct variables, for example do not use $color-text for backgrounds even when you need the same color.
- Variables should be available for colors, font-sizes, line-heights, border-radii, borders, font-families, media-queries.

**Right:**
```SCSS
.selector {
	background-color: $color-background-200;
	color: $color-text-90;
	font-size: $font-size-100;
}
```

**Wrong:**
```SCSS
.selector {
	background-color: $color-text-diap;
	color: red;
	font-size: 16px;
}
```

### Color units should be written in 'HEX', RGBA can be used for transparency

- It's easier to transfer HEX colors to a project as digital design applications often use HEX colors
- Do not abbreviate HEX colors as it decreases readability

**Right:**
```SCSS
#ffffff;
rgba(50, 50, 50, 0.5);
```

**Wrong:**
```SCSS
hsl(120, 100%, 50%);
hsla(120, 100%, 50%, 0.5);
white;
rgb(50, 50, 50);
#fff;
```

### Absolute sizes should be written in pixels instead of ems or rems

- A 'CSS px' is a reference pixel intended to scale in size depending on the 'typical' distance of an observer from the display.
- Web browsers scale a design in pixels the same way they scale designs in ems or rems. Zooming even triggers media queries based on pixels. Essentially, web browsers make the reference pixel larger or smaller.
- Makes it easier to integrate images or other media formats based on pixels in your layout.
- Makes sure you don't get numbers like '0.29310344827586204em' (this is an actual used number).
- Sizing in pixels reduces development time.
- Sizes in ems or rems are allowed, but only when it should actually be based on the font-size. For example a max width of 30 ems to make sure lines never get too long.

See ['W3C Recommendations about lengths'](http://www.w3.org/TR/CSS21/syndata.html#length-units) for further reading.

### Use unitless value for line-height

> Unitless line heights are recommended due to the fact that child elements will inherit the raw number value, rather than the computed value. With this, child elements can compute their line heights based on their computed font size, rather than inheriting an arbitrary value from a parent that is more likely to need overriding.
-- [Sara Cope, 2015](https://css-tricks.com/almanac/properties/l/line-height/)

**Right**
```SCSS
$line-height-100: 1.5;
```

**Wrong**
```SCSS
$line-height-100: 1.5em;
```

### Use the 8-Point Grid as much as possible for pixel values

- Popular screen sizes are divisible by 8.
- Popular icon sizes are divisible by 8.
- Can be easily divided and multiplied to create useful sizes.
- Apple iOS and Google Material Design already use 4- or 8-point system.

See ['The 8-Point Grid'](https://spec.fm/specifics/8-pt-grid) and ['Intro to the 8-Point Grid System'](https://builttoadapt.io/intro-to-the-8-point-grid-system-d2573cde8632) for further reading.


### Use the spacing variable for measurements

- Use a spacing variable in the SCSS settings, to implement the 8-Point Grid.
- When an exception to the 8-Point Grid is needed, the spacing variable is used to calculate the amount of pixels. This means that the largest value possible is calculated by a division or multiplication of the spacing variable and the remaining pixels are substracted or added with hard values.
- When calculating with the spacing variable add spaces around the calculation symbols to improve readability. With multiple calculations add parentheses around each caclulation.

**Right**
```SCSS
$spacing: 8px;

margin: $spacing;
margin: $spacing * 2;
padding: ($spacing * 2) ($spacing * 3);
height: ($spacing * 3) + 2px; //NOTE: 2px extra for borders
margin-right: ($spacing * 4) + ($spacing * 2); //NOTE: Added '$spacing * 2' to account for negative right margin on parent
```

**Wrong**
```SCSS
margin: 8px;
margin: 8px * 2;
margin: $spacing*2;
padding: 8px 24px;
height: 24px + 2px; //NOTE: 2px extra for borders
margin: 32px + 16px; //NOTE: Added 16px to account for negative right margin on parent
```

### Z-indexes are limited to 12 levels

- The z-index starts at -100 and is limited to 1000. Steps are 100.
- Steps of hundreds are used to allow adding additional numbers. But will probably never happen. If more z-index are needed, rethink your code.

**Right:**
```CSS
selector {
	z-index: 200;
}
```

**Wrong:**
```CSS
selector {
	z-index: 248;
}

selector {
	z-index: 9999;
}
```

### Increase Z-indexes inside a component or block with 1

- When a z-index is required inside a component, create a z-index variable for your component.
- The z-index variable can be -100 until 1000 and is a multiple of 100.
- Increase the z-index variable inside your component with 1.

**Right:**
```SCSS
$block-z-index: 300 !default;

block {
	z-index: $block-z-index;
}
block__element {
	z-index: $block-z-index + 1;
}
```

**Wrong:**
```SCSS
block {
	z-index: 300;
}

block__element {
	z-index: 400;
}
```

### Avoid adding units to zero-values

**Right:**
```CSS
selector {
	margin: 0;
}
```

**Wrong:**
```CSS
selector {
	margin: 0px;
}
```

### Always include a leading zero when a numeric value is less than 1

- Do not add trailing zeros.

**Right:**
```CSS
selector {
	margin: 0.5%;
}
```

**Wrong:**
```CSS
selector {
	margin: .50%;
}
```

### Link font weights to their correct CSS values

- Sometimes we encounter fonts that have been given cryptic file names: not containing any clue about the weight or typeface. Rewrite the file names, before you add these to your project. A good pattern would be: [typeface]-[weight].[extension].

**Font weights:**

- 100 = hair
- 200 = thin
- 300 = light
- 400 = normal (or regular, book)
- 500 = medium
- 600 = semi-bold (or demi-bold)
- 700 = bold
- 800 = black (or heavy)
- 900 = ultra

### Write durations in milliseconds
- Writing durations in CSS/SCSS for timing functions in milliseconds so durations in javascript and CSS/SCSS are the same, since javascript internally uses milliseconds.

**Right:**
```scss
.selector {
    opacity: 0;
    transition: opacity 300ms linear;

    &:hover {
         opacity: 1;
    }
}
```
**Wrong:**
```scss
.selector {
    opacity: 0;
    transition: opacity 0.3s linear;

    &:hover {
         opacity: 1;
    }
}
```

### Only use '!important' when you know up front it should always override a style

- Never use '!important' to fix an existing problem.

## Comments

### Use Less/SCSS commenting style '//' for comments pointless for debugging

- Applicable for commenting code not visible in CSS, such as mixins, or variables. It assures you don't have loose comments floating around in dev version: Less/SCSS style comments are always compiled out.
- Comments outside rules should be separated by a single empty line.
- Do not add extra dividers to mark a comment. If needed, change your code coloring to identify comment blocks.
- Use markdown within comments.
- Do not add line breaks for wrapping.

**Right:**
```SCSS
// # Colors

$color-blue: #0000ff; // rgb(0, 0, 255)
```

**Wrong:**
```SCSS
/* -- colors -- */

$color-blue: #0000ff; /* rgb(0, 0, 255) */
```

### Use CSS commenting style '/* */' for comments useful for debugging

- Applicable for commenting code visible in CSS, such as rules, selectors, properties, or values.
- Preserve CSS style comments during compiling Less or SCSS code for dev versions.
- CSS style comments should be removed during compiling Less or SCSS code for live versions.
- Comments outside rules should be separated by a single empty line.
- For comments outsides rules, start and end syntaxes should be on a separate line. Even for single line comments, because of consistency and making transitions between single and multi line (adding and removing lines) easier.
- Comments inside rules (a.k.a. inline comments) can be written as 'single line comment': syntaxes and comment on the same line.
- Do not add extra dividers to mark a section. If needed, change your code coloring to identify comment blocks.
- Do not indent comments or start every line with special characters such as asterisks.
- Use markdown within comments.
- Do not add line breaks for wrapping.

**Right:**
```CSS
/*
# Heading 1
Paragraph text with a [link](url).
*/

/*
Comment on one line outside a rule.
*/

selector {
	property: value; /* Comment on one line inside a rule */
}
```

**Wrong:**
```CSS
/*===
* -- Heading 1 --
* Paragraph
===*/
```

### Numbered labels may be used for inline comments

- Allowed when a rule contains inline comments that are too long to be readable.
- Allowed when a comment is applicable for multiple declarations.
- When using numbered labels for a rule, also use numbered labels for all other inline comments for that rule.

**Right:**
```CSS
/*
Image
1. Makes it responsive.
*/

img {
	max-width: 100%; /* [1] */
	height: auto; /* [1] */
}
```

### Use special tags to mark comments
See a list of available tags in our '[Use special tags to mark comments](../general/README.md#use-special-tags-to-mark-comments)' section in the general conventions.

**Right:**
CSS
```CSS
selector {
	property: value; /* HACK: For Internet Explorer 9 */
}
```
SCSS
```SCSS
selector {
	property: red; // TODO: 2015 04 04: Change value to blue
}
```


### Use KSS for documenting CSS components

To make component based development, generating pattern libraries and reuse of components easier, it is advised to add documentation for each component. For this, you can use [KSS style commenting](https://github.com/kneath/kss) (also see [KSS-node](https://github.com/kss-node/kss-node) or [SC5](https://github.com/SC5/sc5-styleguide)). Because KSS has its own conventions, the conventions for comments written earlier in this document do not apply to KSS comments.

**Right:**
```css
/*
Buttons

A majority of buttons in the site are built from the same base class.

Markup: buttons.hbs

:hover     - Highlight the button when hovered.
:disabled  - Make the button change appearance to reflect it being disabled.
:active    - "Press" the button down when clicked.

Style guide: components - buttons
*/
```

See [KSS](https://github.com/kneath/kss), [KSS-node](https://github.com/kss-node/kss-node), and [SC5](https://github.com/SC5/sc5-styleguide) for further reading.

## Performance

### Prefer first-child over last-child selector

Sometimes you only want to add a margin or border between horizontal items in a collection. This can be done by removing margin-bottom or border-bottom from the last item or removing margin-top or border-top from the first item. Or you can use the `not` selector to skip the first item. For browsers it is far more difficult to select the last-child compared to the first-child, because it has to reselect the last-child every time a new item is loaded/rendered. The first-child can be set immediately. Although it is more intuitive to change the styling of the last-child instead of the first-child. Don't do this, unless there is no other way.

**Right:**
```SCSS
.layout__section {
	margin-top: 40px;

	&:first-child {
		margin-top: 0;
	}
}

.collection__item {

	&:not(:first-child) {
		margin-top: 8px;
	}
}
```

**Wrong:**
```SCSS
.layout__section {
	margin-bottom: 40px;

	&:last-child {
		margin-bottom: 0;
	}
}

.collection__item {

	&:not(:last-child) {
		margin-bottom: 40px;
	}
}
```

## Specific Techniques

### Implement icons for user interface elements with CSS, place icons related to content in HTML

- Icons for user interface elements should be defined by CSS and not placed in the HTML structure. Icons for user interface elements can change based on the status and classes. This can be solved easily with CSS. Defining icons for user interface elements in CSS also makes sure icons are consistent throughout your website or application. You cannot mistakenly use different icons for the same user interface element in different views. Some developers argue these icons are not part of the DOM which reduces accessibility or the ability to add alt text. For user interface elements this should not be an issue. Affordance for user interface elements should never depend on icons and always depend on its shape and visible text or 'hidden text' accessible for screen readers.
- Icons for content, such as icons illustrating product features, should be placed in the HTML. This makes changing your content and icons easier. Furthermore, you don't have to create a new class for every new icon, you only have to change the HTML.

### Overrule :focus style with :focus:hover

- When you use the :focus pseudo-class you can highlight items when they receive focus. This is useful for when the user tabs through a form for example. The :focus styling should be prominent to let a user know where to look. The problem with browsers, such as Google Chrome, is that they also apply the :focus styling when, for example, a button is clicked or touched. In this case the :focus styling is unnecessary noise and should be avoided. Browsers such as Apple Safari don't use :focus styling when a button is clicked or touched. A workaround for the behaviour found in Google Chrome is to use a combination of :focus and :hover pseudo-classes. Override the :focus styling with :focus:hover styling. Because you are always hovering the element when you click on it, it will show the overridden style.

**Example:**
```CSS
.block__element {
    &:focus {
        box-shadow: 0 0 2px -2px $color-focus;

        &:hover {
            box-shadow: none;
        }
    }
}
```

## Acknowledgments and Further Reading

- [sass-guideline.es](http://sass-guidelin.es/#syntax--formatting)
- [cssguidelin.es](http://cssguidelin.es)
- [Medium's Less Coding Guidelines](https://medium.com/@fat/mediums-css-is-actually-pretty-fucking-good-b8e2a6c78b06).
- [Chris Pearce CSS Guidelines](https://github.com/chris-pearce/css-guidelines)
- [Five Q CSS Guidelines](https://github.com/akwright/Five-Q-CSS-Guidelines)
