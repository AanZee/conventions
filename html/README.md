# HTML

## BEM
Structure your components with the [BEM methodology](https://en.bem.info/method/naming-convention/). See [the CSS conventions part](/css/README.md#selector-names-should-follow-bem-methodology-honed-by-nicolas-gallagher) for some of the advantages.

## HTML alignment

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

## Every attribute on a new line

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

## CSS classes as first attribute on the first line

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
When you want to target HTML in JavaScript use attributes prefixed with js-, don't use data-.

**Right:**
```html
<h1 js-component-title>Title</h1>
```

**Wrong:**
```html
<h1 data-component-title>Title</h1>
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