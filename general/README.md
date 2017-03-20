# General conventions
This conventions are best practices in all our programming languages.

## Write in US English
Write your code in US English instead of British English.

## Use tabs instead of spaces
Use tabs instead of spaces when possible in your language. Everyone can use different tab widths in there own editor.

## Don't use author comments
Persons will be switching projects, clients and jobs. You can better use GIT, humans.txt or a README file.

## Be consistent in naming components
Name your files like your components. A SCSS component selector e.g. .blog {} will have the filename _blog.scss. A SCSS mixin beautifulGradient will have the filename _beautiful-gradient.scss. 

## Naming
Use the right naming style per language. We prefer camelCase, PascalCase or dashes.

### camelCase
- JavaScript
- JSON
- ColdFusion
- ColdFusion template translation labels

### PascalCase
- JavaScript classes

### Dashes
- CSS selectors
- Angular template translation labels


## Naming booleans
Prefix booleans always with: is, has or should.

**Right:**
```javascript
let isA = true;
let hasB = false;
let shouldC = true;
```

**Wrong:**
```javascript
let a = true;
let b = false;
let c = true;
```

## Spaces between function parameters
Always split parameters by one space.

**Right:**
```javascript
function foo(parameter1, parameter2, parameter3) {
}

foo(parameter1, parameter2, parameter3);
```

**Wrong:**
```javascript
function foo(parameter1,parameter2,parameter3) {
}

foo(parameter1,parameter2,parameter3);
```

## Indent source code not output code
In some (template) languages you will have a different indention in your output code than source code. Always write readable source code so it is easier to maintain.

**Right:**
```html
<div>
	<template>
		<h1>Title</h1>
	</template>
</div>
```

**Wrong:**
```html
<div>
	<template>
	 <h1>Title</h1>
	</template>
</div>
```

## Magic numbers
Don't use numbers in your code that don't tell directly what they will do.

**Right:**
```javascript
const maxItems = 3;
if (index < maxItems) {

}
```

**Wrong:**
```javascript
if (index < 3) {
	
}
```

## Remove code, don't comment
When you want to remove some code, remove it. Don't disable it with a comment tag. To reverse the removal, you can use GIT.

**Right:**
```javascript
let a = 1;

console.log(a);
```

**Wrong:**
```javascript
let a = 1;
// let b = 2;

console.log(a);
//console.log(a + b);
```

## Don't write abbreviations
Write full descriptive words.

**Right:**
```css
.button {}
```
```javascript
function superAwesomeFunction() {
}
```


**Wrong:**
```css
.btn {}
```
```javascript
function sprWsmFnctn() {
}
```