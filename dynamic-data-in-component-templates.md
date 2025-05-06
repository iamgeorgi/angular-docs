# Dynamic Data in Component Templates

## String Interpolation
Displays the value of a component property inside the template.
```html
<p>{{ title }}</p>
```

## Property Binding
Binds an element's property to a component property.
```html
<img [src]="imageUrl" />
```

## Event Binding
Executes a method when an event occurs.
```html
<button (click)="onClick()">Click Me</button>
```

## Two-Way Binding
Synchronizes input field value with a component property.
```html
<input [(ngModel)]="name" />
<p>Your name: {{ name }}</p>
```

Make sure to import `FormsModule` in your module to use `ngModel`.

## Template Reference Variables

Template reference variables (`#var`) allow you to reference a DOM element or component instance directly in your template.

### Example:
```html
<input name="title" id="title" #titleInput />
<button (click)="logTitle(titleInput)">Log Title</button>
```

### Component Method:
```ts
logTitle(input: HTMLInputElement) {
  console.log(input.value);
}
```

You can use the reference to access properties like `.value`, call methods, or pass the element to component logic.

---

Template reference variables can also be used to access:
- Angular components or directives
- Template forms (e.g., `#form="ngForm"`)
- DOM elements directly

They’re only accessible **within the same template** where they’re declared.

## Custom Two-Way Binding

Angular allows you to create your own two-way binding using a combination of `@Input()` and `@Output()` with the `[(binding)]` syntax in the parent.

---

### Traditional `@Input()` / `@Output()` Pattern

#### Child Component
```ts
@Component({
  selector: 'app-rect',
  template: `<button (click)="onReset()">Reset</button>`
})
export class RectComponent {
  @Input() size!: { width: string; height: string };
  @Output() sizeChange = new EventEmitter<{ width: string; height: string }>();

  onReset() {
    this.sizeChange.emit({ width: '100', height: '100' });
  }
}
```

#### Parent Component Template
```html
<app-rect [(size)]="rectSize"></app-rect>
```

#### Parent Component Class
```ts
rectSize = { width: '200', height: '300' };
```

This enables two-way binding on the `size` input, so when the child emits a change, the parent is updated.

---

### Signals-Based Custom Two-Way Binding

#### Child Component
```ts
import { Component, model } from '@angular/core';

@Component({
  selector: 'app-rect',
  standalone: true,
  template: `<button (click)="onReset()">Reset</button>`
})
export class RectComponent {
  size = model<{ width: string; height: string }>();

  onReset() {
    this.size.set({ width: '100', height: '100' });
  }
}
```

This exposes `size` as a signal-enabled input/output pair that supports two-way binding automatically via `[(size)]`.

No need for `@Input()` or `@Output()` — Angular wires it up based on the `model()` declaration.

