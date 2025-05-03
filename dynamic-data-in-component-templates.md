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