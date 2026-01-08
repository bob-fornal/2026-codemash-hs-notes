# 2026 CodeMash Highschool Notes

Site: [https://stackblitz.com](https://stackblitz.com)

## Phase 1: Login & Start Project

1. Signup
2. Select `New project`
3. Select `Angular | TypeScript`

## Phase 2: Add Dependencies (Material)

Add the following to `package.json`:

```json
  "@angular/material": "^21.0.0",
  "@angular/cdk": "^21.0.0"
```

Run `npm install && npm start` in the Terminal.

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
    <h1>Hello from {{ name }}!</h1>
    <!-- <a target="_blank" href="https://angular.dev/overview">
      Learn more about Angular
    </a> -->
    <button matButton="filled" color="primary" (click)="handleLearnClick()">Learn more about Angular</button>
  `,
})
export class App {
  name = 'Angular';

  handleLearnClick() {
    console.log('live');
  }
}

bootstrapApplication(App);
```

Additionally, change the `global_styles.css` to include:

```css
@import '@angular/material/prebuilt-themes/indigo-pink.css';
```
