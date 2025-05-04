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

You can also use CSS-style selectors to match multiple element types. For example:

```html
<ng-content select="input, textarea"></ng-content>
```

This will match both `<input>` and `<textarea>` elements in the projected content.

## Accessing Template Elements with `@ViewChild` and `@ViewChildren`

### `@ViewChild` — Access a Single Element or Component
The `@ViewChild` decorator lets you access a template reference or child component directly from the class.

#### Example: Access a Form Element
```ts
@ViewChild('form') form?: ElementRef<HTMLFormElement>;

onSubmit() {
  this.form?.nativeElement.reset(); // Reset the form
}
```

#### Template
```html
<form #form="ngForm" (ngSubmit)="onSubmit()">
  <!-- form contents -->
</form>
```

---

### `@ViewChildren` — Access Multiple Elements or Components
Use `@ViewChildren` to query a list of matching elements or components.

#### Example:
```ts
@ViewChildren('item') items!: QueryList<ElementRef<HTMLDivElement>>;

ngAfterViewInit() {
  this.items.forEach(el => {
    el.nativeElement.classList.add('loaded');
  });
}
```

#### Template
```html
<div #item *ngFor="let i of [1, 2, 3]">Item {{ i }}</div>
```

---

### Signals-Based Alternative: `viewChild` and `viewChildren`
Angular also provides **Signal-compatible** versions of these decorators.

#### `viewChild` Example:
```ts
form = viewChild('form');

onSubmit() {
  this.form()?.nativeElement.reset();
}
```

#### `viewChildren` Example:
```ts
items = viewChildren('item');

ngAfterViewInit() {
  this.items().forEach(el => {
    el.nativeElement.classList.add('loaded');
  });
}
```

These alternatives are useful when working in a signal-based component or trying to avoid decorators.

## Accessing Projected Content with `@ContentChild` and `@ContentChildren`

### `@ContentChild` — Access a Single Projected Element or Component
Use `@ContentChild` to get a reference to a projected element inside an `<ng-content>` slot.

#### Example:
```ts
@ContentChild('projectedButton') button?: ElementRef<HTMLButtonElement>;

ngAfterContentInit() {
  this.button?.nativeElement.classList.add('highlight');
}
```

#### Template (Child Component)
```html
<div class="card">
  <ng-content></ng-content>
</div>
```

#### Usage (Parent Component)
```html
<app-card>
  <button #projectedButton>Click me</button>
</app-card>
```

---

### `@ContentChildren` — Access Multiple Projected Elements
Use this when you expect multiple elements inside `ng-content`.

#### Example:
```ts
@ContentChildren('section') sections!: QueryList<ElementRef>;

ngAfterContentInit() {
  this.sections.forEach(el => el.nativeElement.classList.add('section-ready'));
}
```

#### Usage
```html
<app-layout>
  <div #section>Header</div>
  <div #section>Body</div>
</app-layout>
```

---

### Signal-Based Alternatives: `contentChild` and `contentChildren`

#### `contentChild` Example:
```ts
projectedButton = contentChild('projectedButton');

ngAfterContentInit() {
  this.projectedButton()?.nativeElement.focus();
}
```

#### `contentChildren` Example:
```ts
sections = contentChildren('section');

ngAfterContentInit() {
  this.sections().forEach(el => el.nativeElement.classList.add('ready'));
}
```

These are reactive alternatives to decorators, ideal for signal-based components and better composability.
