# Pipes

## Built-in Pipes
Transform data in templates.

```html
<p>{{ today | date: 'short' }}</p> <!-- Formats date to a short format -->
<p>{{ amount | currency: 'USD' }}</p> <!-- Formats number as currency -->
<p>{{ message | uppercase }}</p> <!-- Converts to uppercase -->
```

### Common Built-in Pipes
- `date`: formats date values.
- `currency`: formats numbers as currency.
- `uppercase` / `lowercase`: transforms string case.
- `json`: converts object to JSON string.

Pipes help present data in a more readable or formatted way in templates.