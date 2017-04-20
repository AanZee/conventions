# Angular 2

## Naming
For components, directives, services, providers, helpers, reducers, interfaces etc., use the following naming conventions:

- For components: don't use `SomeComponent.ts` or `some-component.ts`, use `some.component.ts`
- For unit test spec files, use `some.component.spec.ts`
- For view template files, use `some.component.html`

## File ordering
For components, store all the files that have to do with your component in their same respective directory. The same goes for directives, services, providers, helpers, reducers, interfaces etc.:

**Right:**
```
app
├──components
|  ├──some-view
|  |  ├──header
|  |  |  ├──header.component.html
|  |  |  ├──header.component.spec.ts
|  |  |  ├──header.component.ts
|  ├──some-view.component.html
|  ├──some-view.component.spec.ts
|  ├──some-view.component.ts
```

**Wrong:**
```
app
├──components
|  ├──some-view
|  |  ├──some-view.component.ts
|  ├──header
|  |  ├──header.component.ts
├──templates
|  ├──some-view
|  |   ├──some-view.component.html
|  ├──header
|  |  ├──header.component.html
├──tests
|  ├──some-view
|  |  ├──some-view.component.spec.ts
|  ├──header
|  |  ├──header.component.spec.ts
```

## Exports and imports
Don't use default exports in Angular files, no matter how much a good idea they seem.

**Right:**
```ts
export class SomeComponent {}
```

**Wrong:**
```ts
export default class SomeComponent {}
```
Leave an empty line between native Angular and native library imports and custom imports, like so:

```ts
import { Component, Input, Output } from '@angular/core';
import { Store } from '@ngrx/store';

import { SomeService, AnotherService } from '../../services';
import { SomeHelper } from '../../helpers';
```

Only use the require statement to import a module if the dependency doesn't support the new Node import/export notation:

```ts
import { Component } from '@angular/core';
const SomeLibrary = require('some-library'); // etc.
```

## Components

Always use a separate file for your view template. Do not write your HTML in the Component decorator:

**Right:**
```ts
import { Component } from '@angular/core';

@Component({
	selector: 'some-component',
	templateUrl: 'some.component.html'
})
export class SomeComponent {}
```

**Wrong:**
```ts
import { Component } from '@angular/core';

@Component({
	selector: 'some-component',
	template: `
	<div class="some-somponent">
		<header class="some-component__header">
			Etc.
		</header>
	</div>
	`
})
export class SomeComponent {}
```

Don't use require statements for your templates or styles, use templateUrls and styleUrls. In Webpack, the Angular 2 template-loader plugin will change it to require at build time anyway:

**Right:**
```ts
@Component({
	selector: 'some-component',
	templateUrl: 'some.component.html',
	styleUrl: 'some.component.css'
})
```

**Wrong:**
```ts
@Component({
	selector: 'some-component',
	template: require('./some.component.html'),
	style: require('./some.component.css'),
})
```

## Forms

- Don't use `form.controls.controlName`, use `form.get('controlName)'`
- Don't use `control.errors?.someError`, use `control.hasError('someError')`

## Templates

### ngIf as second HTML attribute
Write an ngIf tag as second HTML attribute after the class attribute. Or as first attribute when there is no class available.

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

### Don't use empty divs for templates

**Right:**
```html
<template [ngIf]="true">
    <h1>Component</h1>
</template>

<h1 *ngIf="true">Component</h1>
```

**Wrong:**
```html
<div *ngIf="true">
    <h1>Component</h1>
</div>
```