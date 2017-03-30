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
Don't use lists as container for a lot of data, only for simple lists.

**Right:**
```html
<h1>Components</h1>
<ul>
    <li>Component 1</li>
    <li>Component 2</li>
    <li>Component 3</li>
</ul>
```

**Wrong:**
```html
<h1>Components</h1>
<ul class="component">
    <li class="component__item">
        <div class="component__item-inner">
            <h1 class="component__item-title">Component 1</h1>
            <p class="component__item-text">Component description</p>
        </div>
    </li>
    <li class="component__item">
        <div class="component__item-inner">
            <h1 class="component__item-title">Component 2</h1>
            <p class="component__item-text">Component description</p>
        </div>
    </li>
    <li class="component__item">
        <div class="component__item-inner">
            <h1 class="component__item-title">Component 3</h1>
            <p class="component__item-text">Component description</p>
        </div>
    </li>
</ul>
```