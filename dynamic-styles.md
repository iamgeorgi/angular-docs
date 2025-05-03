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

## Styling with `:host` and Setting Host Classes

### Using `:host` in Component Styles
```css
:host {
  display: block;
  padding: 1rem;
  border: 1px solid #ccc;
}
```

Targets the component's host element from inside its style file.

---

### Setting Host Class via `host` Metadata
```ts
@Component({
  selector: 'app-control',
  template: `<ng-content></ng-content>`,
  host: {
    class: 'control'
  }
})
export class ControlComponent {}
```

Applies the `control` class to the component’s root element.

---

### Setting Host Class via `@HostBinding`
```ts
@Component({
  selector: 'app-control',
  template: `<ng-content></ng-content>`
})
export class ControlComponent {
  @HostBinding('class') className = 'control';
}
```

Also sets a class on the host element, but allows dynamic updates based on component logic.

## Class and Style Bindings in Templates

### Binding Single Class Conditionally
```html
<div [class.status]="currentStatus === 'offline'">Offline</div>
```

Adds the `status` class only when the condition is true.

---

### Binding Multiple Classes Conditionally
```html
<div [ngClass]="{
  status: true,
  'status-online': currentStatus === 'online',
  'status-offline': currentStatus === 'offline',
  'status-unknown': currentStatus === 'unknown'
}">
  Status: {{ currentStatus }}
</div>
```

Applies multiple classes dynamically based on component state.

---

### Binding Inline Styles Dynamically
```html
<div [style.height]="(dataPoint.value / maxTraffic) * 100 + '%'">
  Traffic Bar
</div>
```

Binds a calculated height to the element based on data.

