# Services

## Creating a Service
A service is used to share logic and data across components.
```typescript
import { Injectable } from '@angular/core';

@Injectable({ providedIn: 'root' })
export class ExampleService {
  getData() {
    return 'Service Data';
  }
}
```

## Injecting via Constructor
Injects a service into a component via constructor.
```typescript
import { Component } from '@angular/core';
import { ExampleService } from './example.service';

@Component({ selector: 'app-root', template: `<p>{{ data }}</p>` })
export class AppComponent {
  data: string;

  constructor(private exampleService: ExampleService) {
    this.data = this.exampleService.getData();
  }
}
```

## Injecting via `inject()`
Alternative approach using `inject()` function for dependency injection.
```typescript
import { inject } from '@angular/core';

export class AnotherComponent {
  private exampleService = inject(ExampleService); // Inject service using inject()
  data = this.exampleService.getData();
}
```

Services promote reusable logic and centralize shared state.