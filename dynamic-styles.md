# Dynamic Styles

## Dynamic CSS Classes and Styles
Apply styles or classes conditionally or dynamically.

```html
<p [class.highlight]="isHighlighted">Styled text</p>
<!-- Applies 'highlight' class if isHighlighted is true -->

<p [ngStyle]="{ 'color': textColor }">Styled text</p>
<!-- Applies dynamic color based on textColor property -->
```

You can also bind multiple classes dynamically:
```html
<div [ngClass]="{ 'active': isActive, 'disabled': !isEnabled }"></div>
```

This allows for responsive and state-based styling of elements in templates.