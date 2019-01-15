# ColdFusion

## Ortus ColdFusion (CFML) Standards & Best Practices
Along with the conventions reported below, we follow the [Ortus ColdFusion (CFML) Standards & Best Practices](https://github.com/Ortus-Solutions/coding-standards/blob/master/coldfusion.md) conventions.

## Write all condition operators in capitals

**Right:**
```html
<cfif a EQ 1 OR b EQ 2>
```

**Wrong:**
```html
<cfif a eq 1 or b eq 2>
```

## Don't write cfif's inside HTML attributes

**Right:**
```html
<cfif a EQ 1>
	<cfset classNames="component"/>
<cfelse>
	<cfset classNames="component component--modifier"/>
</cfif>

<h1 class="#classNames#">A</h1>
```

**Wrong:**
```html
<h1 class="component<cfif a EQ 1> component--modifier</cfif>">A</h1>

<h1 class="component #iif(a EQ 1, DE(''), DE('component--modifier'))#">A</h1>
```

## Close self-closing tags with a forward slash
Always close self-closing tags with a forward slash. It makes the code more readable; you instantly see the tag is not a block of code. Also, if you use custom tags, there is a difference in behaviour: https://stackoverflow.com/a/7544785.

**Right:**
```html
<cfset var test = "test"/>

<cfdump var="#test#"/>
```

**Wrong:**
```html
<cfset var test = "test">

<cfdump var="#test#">
```

### Exception
Closing custom tags will be executed twice. For example closing the 'cfmodule' tag will insert the given template twice. Because of this we can't close these tags.
https://groups.google.com/forum/#!topic/railo/tcZoBiZnDGU

## Put HTML attributes inside a cfif on a new line

**Right:**
```html
<div
	<cfif test EQ "test">
		data-test="test"
	</cfif>
>
```

**Wrong:**
```html
<div
	<cfif test EQ "test">data-test="test"</cfif>
>
```
