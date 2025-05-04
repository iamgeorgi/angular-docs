# Angular Lifecycle Hooks

Angular provides lifecycle hooks that allow you to tap into different phases of a component's existence.

---

## `ngOnInit()`

Called once after the component's inputs are initialized.

### Example:
```ts
ngOnInit() {
  console.log('Component initialized');
}
```

Use this for:
- Initializing data
- Fetching data from services
- Setting up logic that only runs once

---

## `ngOnChanges(changes: SimpleChanges)`

Called whenever an input-bound property changes.

### Example:
```ts
@Input() userId!: number;

ngOnChanges(changes: SimpleChanges) {
  if (changes['userId']) {
    console.log('User ID changed:', changes['userId'].currentValue);
  }
}
```

Use this when:
- You need to react to input property changes
- You want to compare previous and current values

---

## `ngAfterViewInit()`

Called once after the component's view (and child views) have been fully initialized.

### Example:
```ts
@ViewChild('input') inputRef!: ElementRef;

ngAfterViewInit() {
  this.inputRef.nativeElement.focus();
}
```

Use this to safely access:
- `@ViewChild` or `@ViewChildren` elements
- DOM-related logic after rendering

---

## `ngAfterContentInit()`

Called after projected content (`ng-content`) has been initialized.

### Example:
```ts
@ContentChild('slotContent') slot!: ElementRef;

ngAfterContentInit() {
  console.log('Projected content initialized');
}
```

Use this when working with:
- Content projection
- `@ContentChild` or `@ContentChildren`

---

## `ngOnDestroy()`

Called just before the component is destroyed. Use it to clean up subscriptions, intervals, or external resources.

### Example: Clear `setInterval`
```ts
intervalId!: number;

ngOnInit() {
  this.intervalId = setInterval(() => {
    console.log('Polling...');
  }, 1000);
}

ngOnDestroy() {
  clearInterval(this.intervalId);
}
```

---

### Alternative: Use `DestroyRef` for Cleanup
```ts
import { inject, DestroyRef } from '@angular/core';

private destroyRef = inject(DestroyRef);

constructor() {
  const intervalId = setInterval(() => {
    console.log('Polling with DestroyRef');
  }, 1000);

  this.destroyRef.onDestroy(() => clearInterval(intervalId));
}
```

This avoids manually implementing `OnDestroy`, and works well with composables or services.

---
