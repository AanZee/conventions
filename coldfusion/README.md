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