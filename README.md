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

## Phase 4: Move Search to a Component

Create a folder, `scr\pages`. Then, create a folder inside that called `search`.

You will want three files:

* `search-component.css`
* `search-component.html`
* `search-componnent.ts`

`search-component.ts` should be as follows.

```typescript
import { Component } from '@angular/core';
import { MatButtonModule } from '@angular/material/button';

@Component({
  selector: 'app-search-component',
  imports: [MatButtonModule],
  templateUrl: './search-component.html',
  styleUrls: ['./search-component.css'],
})
export class SearchComponent {
  handleClick() {
    console.log('live');
  }
}
```

The `search-component.html` will be as follows.

```html
<h1>TCG Card Application</h1>

<button matButton="filled" color="primary" (click)="handleClick()">
  Start
</button>
```

And, finally, adjust `main.ts` as follows.

```typescript
import { Component } from '@angular/core';
import { bootstrapApplication } from '@angular/platform-browser';
import { SearchComponent } from './pages/search/search-component';

@Component({
  selector: 'app-root',
  imports: [SearchComponent],
  template: `<app-search-component />`,
})
export class App {}

bootstrapApplication(App);
```
