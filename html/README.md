# HTML

## BEM
Structure your components with the [BEM methodology](https://en.bem.info/method/naming-convention/). See [the CSS conventions part](/css/README.md#selector-names-should-follow-bem-methodology-honed-by-nicolas-gallagher) for some of the advantages.

## HTML Head

The following 2 meta tags *must* come first in the ```<head>``` to consistently ensure proper document rendering.

**Right:**
```html
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">

<title>Page Title</title>
```

A comprehensive guide to everything that can be placed in the ```<head>``` can be found on [gethead](https://gethead.info/).

## Write HTML and content on new lines

**Right:**
```html
<h1 class="component"
    id="component"
>
    Title
</h1>
```

**Wrong:**
```html
<h1 class="component"
    id="component">
    Title
</h1>

<h1 class="component"
    id="component">Title
</h1>

<h1 class="component"
    id="component">Title</h1>

<h1 class="component" id="component">Title</h1>
```

### Textarea exception
For textarea tags, do not place the closing tag </textarea> on a new line, as it adds spaces within the input.

**Right:**
```html
<textarea class="component"
    id="component"
></textarea>
```

**Wrong:**
```html
<textarea class="component"
    id="component"
>
</textarea>
```

## Write every attribute on a new line

**Right:**
```html
<h1 class="component"
    id="component"
>
    Title
</h1>
```

**Wrong:**
```html
<h1 class="component" id="component">
    Title
</h1>

<h1
    class="component"
    id="component"
>
    Title
</h1>
```

### Write CSS classes as first attribute on the first line

**Right:**
```html
<h1 class="component"
    id="component"
>
    Title
</h1>
```

**Wrong:**
```html
<h1 id="component"
    class="component"
>
    Title
</h1>

<h1
    class="component"
    id="component"
>
    Title
</h1>
```

## Always use a button element for buttons
Never use an input element for buttons. A button element is more flexible. It can be part of a form, but doesn't have to. Useful for when a clickable element does not have a meaningful link. Also, a button element can contain other content, such as pseudo-elements.

**Right:**
```html
<button type="button">Press me!</button>
```

**Wrong:**
```html
<input type="button" value="Press me!">
```

## Add type to button elements
Always add a type to a button to prevent accidentally submitting forms

**Right:**
```html
<button type="button">Button</button>
<button type="submit">Button</button>
```

**Wrong:**
```html
<button>Button</button>
```

## Prefix JavaScript attributes
When you want to target HTML in JavaScript use attributes prefixed with data-.

**Right:**
```html
<h1 data-component-title>Title</h1>
```

**Wrong:**
```html
<h1 js-component-title>Title</h1>
<h1 component-title>Title</h1>
```

## Only use lists for simple lists
- Don't use lists as container for a lot of data, only for simple lists.
- Use HTML lists only for bullet or numbered lists in for example content area's. Don't use it for components that don't look like a list, such as a menu or a collection of cards. A lot of front-end developers still use 'ul' and 'li' to structure collections such as toolbar items or menu items. [This makes it harder for users with screen readers to navigate through your website](https://css-tricks.com/navigation-in-lists-to-be-or-not-to-be/). Components don't require additional structure to make it clear to users with screen readers, HTML is already structured and 'the additional structure' creates only more noise.

**Right:**
```html
<ul>
    <li>List item</li>
    <li>List item</li>
    <li>List item</li>
</ul>
```

**Wrong:**
```html
<ul class="collection">
    <li class="collection__item">
        <div class="card">
            <h1 class="card__title">Title</h1>
            <p class="card__text">Description</p>
        </div>
    </li>
    <li class="collection__item">
        <div class="card">
            <h1 class="card__title">Title</h1>
            <p class="card__text">Description</p>
        </div>
    </li>
    <li class="collection__item">
        <div class="card">
            <h1 class="card__title">Title</h1>
            <p class="card__text">Description</p>
        </div>
    </li>
</ul>
```
