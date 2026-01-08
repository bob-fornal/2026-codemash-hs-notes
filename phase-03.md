## Phase 3: Use a Button

In the file `src\main.ts`, change it to match the follwing.

```typescript
import { Component } from '@angular/core';
import { bootstrapApplication } from '@angular/platform-browser';

import { MatButtonModule } from '@angular/material/button';

@Component({
  selector: 'app-root',
  imports: [MatButtonModule],
  template: `
    <h1>TCG Card Application</h1>
    <button matButton="filled" color="primary" (click)="handleClick()">Start</button>
  `,
})
export class App {
  handleClick() {
    console.log('live');
  }
}

bootstrapApplication(App);
```

Additionally, change the `global_styles.css` to include:

```css
@import '@angular/material/prebuilt-themes/indigo-pink.css';
```
