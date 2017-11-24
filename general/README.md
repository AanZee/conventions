# General
These conventions are best practices in all our programming languages.

## Write in US English
Write your code in US English instead of British English. E.g. color instead of colour.

### Use .editorconfig
EditorConfig helps developers define and maintain consistent coding styles between different editors and IDEs. An [editorconfig](.editorconfig) file with our defined conventions can be found in this folder.

A list of [available plugins](http://editorconfig.org/#download) for almost all editors can be found online.

### Indents should be done with tabs instead of spaces
Use tabs instead of spaces when possible in your language.
- Tabs allow developers with different preferences in indentation size to change how the code looks.
- It is impossible to half-indent with tabs.
- Requires less interaction.

**Right:**
```CSS
selector {
	property: value;
}
```

**Wrong:**
```CSS
selector {
 property: value;
}
```

## Never break code lines
- Some guidelines advice to break lines after 80 characters for readability. Don't do this.
- Line breaks have or should have semantic value.
- Manually limiting line length adds unnecessary extra time for editing comments.
- Set your editor to wrap lines instead.

## Don't add author comments
Persons will be switching projects, clients and jobs. You can better use Git, humans.txt or a README file when you want to share contact information.

**Wrong:**
```javascript
/**
 * Awesome code block
 * @author Name <name@company.com>
 */
 ```

## Be consistent in naming components
Name your files like your components. A SCSS component selector e.g. .blog {} will have the filename _blog.scss. A SCSS mixin beautifulGradient will have the filename _beautiful-gradient.scss.

## Naming
Use the right naming style per language. We prefer dashes, camelCase or PascalCase.

### Dashes
- CSS selectors
- Angular template translation labels
- Git branches
- File names
- Folder names

### camelCase
- JavaScript
- JSON
- ColdFusion
- ColdFusion template translation labels

### PascalCase
- JavaScript classes

## Use special tags to mark comments
- Using consistent tags such as 'TODO' makes sure they can be easily found with text search.
- For TODOs include a date when it should be done if possible.
- Always start TODOs with a verb.
- Move TODOs as soon as possible to your backlog.

**Available tags**
- NOTE: a explanation to other developers.
- TODO: a task that should be done in the near future.
- BUG: something that should be done as soon as possible.
- HACK: fix for a specific web browser or situation.
- DEBUG: A temporary comment.
- IDEA: Possible improvement.
- ???: Unclear, needs a better description.
- CRED: Credits for someone.

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

## Comma-separated values should include a space after each comma

**Right:**
```javascript
function foo(parameter1, parameter2, parameter3) {}

foo(parameter1, parameter2, parameter3);
```

**Wrong:**
```javascript
function foo(parameter1,parameter2,parameter3) {}

foo(parameter1,parameter2,parameter3);
```

## There should be no trailing white spaces
Turn on 'show invisibles' to find and remove trailing white spaces/tabs.

## Every file should end with an empty line
You can add a plugin to your IDE that does this for you.

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

## Remove unused code
When you want to remove some code, remove it. Don't disable it with a comment tag. To reverse the removal, you can use Git.

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
- Write full descriptive words.
- Shorter names could lead to misunderstandings.
- Shorter names don't affect file size that much, because of how GZIP works.

**Right:**
```css
.button {}
```
```javascript
function superAwesomeFunction() {}
```


**Wrong:**
```css
.btn {}
```
```javascript
function sprWsmFnctn() {}
```

## Descriptive naming
Use names that explain the functionality or data format.

**Right:**
```javascript
let itemList = [];

function getItemList() {
	return itemList;
}
```
**Wrong:**
```javascript
let someName = [];

function doSomething() {
	return someName;
}
```
