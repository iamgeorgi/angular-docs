# Component Communication

## Input and Output
Allows data to be passed from parent to child (`@Input`) and vice versa (`@Output`).

### Child Component
```typescript
import { Component, Input, Output, EventEmitter } from '@angular/core';

@Component({
  selector: 'app-child',
  template: `<p>{{ message }}</p>
             <button (click)="sendData()">Send Data</button>`
})
export class ChildComponent {
  @Input() message!: string; // Receive data from parent
  @Output() messageEvent = new EventEmitter<string>(); // Emit data to parent

  sendData() {
    this.messageEvent.emit('Hello from Child');
  }
}
```

### Parent Component
```typescript
@Component({
  selector: 'app-parent',
  template: `<app-child [message]="parentMessage" (messageEvent)="receiveMessage($event)"></app-child>`
})
export class ParentComponent {
  parentMessage = 'Hello from Parent';
  receiveMessage(event: string) {
    console.log(event); // Logs data received from child
  }
}
```

## Input and Output with Signals
Angular Signals provide a reactive approach to state management. They can also be used to pass reactive values.

```typescript
import { signal } from '@angular/core';

export class SignalComponent {
  message = signal('Hello from Angular Signals'); // Reactive variable
}
```

*More advanced usage of Signals for communication is possible with shared reactive state via services.*

## Signals
Signals are Angular’s new reactive primitives, offering fine-grained reactivity like Solid.js.

```typescript
import { signal, computed, effect } from '@angular/core';

@Component({
  selector: 'app-signals',
  template: `
    <input [value]="name()" (input)="updateName($event.target.value)" />
    <p>Hello, {{ greeting() }}!</p>
  `
})
export class SignalsComponent {
  name = signal('Angular');
  greeting = computed(() => `Welcome, ${this.name()}!`);

  updateName(newName: string) {
    this.name.set(newName);
  }

  constructor() {
    effect(() => console.log(this.greeting()));
  }
}
```

- `signal`: reactive variable.
- `computed`: derives value reactively.
- `effect`: side effect that auto-runs when dependencies change.