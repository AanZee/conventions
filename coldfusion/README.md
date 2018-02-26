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

## Don't write cfif's in HTML tags

**Right:**
```html
<cfif a EQ 1>
    <cfset classNames="component">
<cfelse>
    <cfset classNames="component component--modifier">
</cfif>

<h1 class="#classNames#">A</h1>
```

**Wrong:**
```html
<h1 class="component<cfif a EQ 1> component--modifier</cfif>">A</h1>

<h1 class="component #iif(a EQ 1, DE(''), DE('component--modifier'))#">A</h1>
```

## Close self-closing tags with a forward slash

Always close self-closing tags with a forward slash. It makes the code more readable; you instantly see the tag is not a block of code. Also if you use custom tags there is a difference in behaviour:

**Take this custom tag:**
```html
<cfif thisTag.ExecutionMode EQ "start">
    started<br/>
</cfif>

running<br/>

<cfif thisTag.ExecutionMode EQ "end">
    ended<br/>
</cfif>
```

**This invocation:**
```html
<p>&lt;cf_demo&gt;</p>

<cf_demo>

<p>&lt;cf_demo /&gt;</p>

<cf_demo />
```

**This is the output:**
```html
<cf_demo>
started
running

<cf_demo />
started
running
running
ended
```

So, the second syntax is the equivalent of <cf_demo></cf_demo>.
* *Source: https://stackoverflow.com/a/7544785* *

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