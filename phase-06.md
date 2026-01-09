# Phase 6: Create a search bar

1. In the `search-component.html` file, we will add code to display the search input and modify the button to trigger the search.

```html
<h1>TCG Card Application</h1>

<form class="search-form">
  <mat-form-field class="search-full-width">
    <mat-label>Pokemon Name</mat-label>
    <input matInput placeholder="Ex. Dark Abra">
  </mat-form-field>

  <button matButton="filled" color="primary" (click)="handleClick()">
    Search
  </button>  
</form>
```

2. Add the follwing CSS to the `search-component.css` to adjust the width of the input.

```css
.search-full-width {
  width: 80%;
}
```

3. Since there should still be an error, we need to correct the `search-component.ts` as follows. **Note the imports, constructor, and `handleClick` function.**

```typescript
import { Component } from '@angular/core';

import { MatButtonModule } from '@angular/material/button';
import { MatInputModule } from '@angular/material/input';

import { ApiService } from '../../core/services/api-service';

@Component({
  selector: 'app-search-component',
  imports: [MatButtonModule, MatInputModule],
  templateUrl: './search-component.html',
  styleUrls: ['./search-component.css'],
})
export class SearchComponent {
  constructor(
    private apiService: ApiService
  ) {
  }

  handleClick() {
    this.apiService.init();
  }
}
```

With the code, as it is, you can click the ***Search** button and the `init` function in the API service will fire.
