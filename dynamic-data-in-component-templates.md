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