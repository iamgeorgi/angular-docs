# Content Projection

## Using `ng-content`
Allows child components to project content into a placeholder in the parent component.

### Component Template (Parent)
```html
<ng-content></ng-content>
```

### Usage Example (Child HTML)
```html
<app-card>
  <p>Content inside projected slot</p>
</app-card>
```

This enables reusable components where part of the content is customizable by the parent using it.

## Using Multiple `ng-content` with `ngProjectAs`  
Projects content into specific slots using attribute selectors. `ngProjectAs` lets you target a slot without adding attributes directly to the HTML.

### Component Template (Parent)
```html
<div class="card">
  <ng-content select="[card-title]"></ng-content>
  <ng-content select="[card-body]"></ng-content>
</div>
```

### Usage Example (Child HTML)
```html
<app-card>
  <h3 ngProjectAs="[card-title]">Projected Title</h3>
  <p ngProjectAs="[card-body]">Projected Body</p>
</app-card>
```

This allows projecting elements into the correct slots without adding custom attributes like `card-title` or `card-body` directly to the DOM.