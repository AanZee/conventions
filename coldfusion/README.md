# ColdFusion

## Write all condition separators in capitals

**Right:**
```html
<cfif a EQ 1 OR b EQ 2>
```

**Wrong:**
```html
<cfif a eq 1 or b eq 2>
```

## Don't write cfif in HTML tags

**Right:**
```html
<cfif a eq 1>
    <h1 class="component">A</h1>
<cfelse>
    <h1 clas="component component--modifier">A</h1>
</cfif>
```

**Wrong:**
```html
    <h1 class="component<cfif a eq 1> component--modifier</cfif>">A</h1>
```