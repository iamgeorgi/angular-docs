# Directives

## Built-in Directives

### `*ngIf` and Alternative `@if`
Conditionally displays elements based on a condition.
```html
<p *ngIf="isVisible">This is conditionally visible</p>
```
```html
@if (isVisible) { <p>This is conditionally visible</p> }
```

### `*ngFor` and Alternative `@for`
Iterates over an array and displays a list of elements.
```html
<li *ngFor="let item of items">{{ item }}</li>
```
```html
@for (item of items; track item.id) { <li>{{ item }}</li> }
```

These directives are commonly used for conditionally displaying or repeating content in templates.