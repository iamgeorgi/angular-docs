# Angular Components

## Creating a Component with the `@Component` Decorator
Components are the building blocks of an Angular application. They define the structure and behavior of a UI element.

```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'app-example',
  template: `<h1>Hello, Angular!</h1>`,
  styles: [`h1 { color: blue; }`]
})
export class ExampleComponent {}
```

- `selector`: the name used to place the component in HTML.
- `template`: defines the inline HTML template.
- `styles`: optional inline styles.

---

## Component Selectors with Attribute Conditions  
Angular allows you to define selectors that match both an element and an attribute. This is useful for applying a component to standard HTML elements like `<button>` or `<input>`.

### Example: `selector: 'button[someSelector]'`
In the component:
```ts
@Component({
  selector: 'button[someSelector]',
  template: `<ng-content></ng-content>`,
  styleUrls: ['./custom-button.component.css']
})
export class CustomButtonComponent {}
```

This component will only activate on a `<button>` element that has the `someSelector` attribute.

### Usage Example
```html
<!-- This will use CustomButtonComponent -->
<button someSelector>
  Click me
</button>

<!-- This will NOT use CustomButtonComponent -->
<button>
  I’m just a normal button
</button>
```

This pattern is great for enhancing native elements without requiring a custom tag, keeping your HTML clean and semantic.


