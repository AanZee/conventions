# SVG

## Optimize SVG code
When using svg files in your project, optimize them according to the following standards:
- Place SVG's on a 32px by 32px grid
- Place vector points on the pixel grid as much as possible
- Round coordinates and vectors up to two decimal places, for example 10.45132 becomes 10.45
- Remove width and height, when needed add this to HTML or CSS.

**Right:**
```svg
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 32 32">
	<path fill="" d="M7.45,2.64 C6.85,2.04 6.85,1.06 7.45,0.45 C8.05,-0.15 9.02,-0.15 9.62,0.45 L25,16 L9.62,31.55 C9.02,32.15 8.05,32.15 7.45,31.55 C6.85,30.94 6.85,29.96 7.45,29.36 L20.67,16 L7.45,2.64 Z"/>
</svg>
```

**Wrong:**
```svg
<svg xmlns="http://www.w3.org/2000/svg" width="32" height="32">
	<path fill="" d="M7.45342,2.64 C6.85123,2.04234 6.85,1.06 7.451234,0.451234 C8.051231,-0.1534 9.02,-0.1523 9.62,0.45479 L25,16125 L9.62,31.55234 C9.02,32.15 8.05,32.15 7.45,31.55234 C6.85,30.944356 6.85,29.964536 7.45,29.36859 L20.67,16241 L7.45,2.64327 Z"/>
</svg>
```