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
