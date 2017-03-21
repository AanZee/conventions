# Angular

## ngIf as second HTML attribute
Write a ngIf tag as second HTML attribute after the class attribute. Or as first attribute when there is no class available.

**Right:**
```html
<div class="component"
    *ngIf="true"
    id="component"
>
    <h1>Component</h1>
</div>

<div *ngIf="true"
    id="component"
>
    <h1>Component</h1>
</div>
```

**Wrong:**
```html
<div id="component"
    *ngIf="true"
    class="component"    
>
    <h1>Component</h1>
</div>

<div id="component"
    *ngIf="true"
>
    <h1>Component</h1>
</div>
```

## Don't use empty divs for templates

**Right:**
```html
<div *ngIf="true"
    id="component"
>
    <h1>Component</h1>
</div>
```

**Wrong:**
```html
<div id="component"
    *ngIf="true"
    class="component"    
>
    <h1>Component</h1>
</div>

<div id="component"
    *ngIf="true"
>
    <h1>Component</h1>
</div>
```