# Phase 7: Connect the search bar to the API Service correctly

1. Import `FormsModule` to the component (`search-component.ts`).
2. Add `FormsModule` as an import (`search-component.ts`).
3. Define the variable called `searchName` (`search-component.ts`).

```typescript
import { Component } from '@angular/core';

import { FormsModule } from '@angular/forms';
import { MatButtonModule } from '@angular/material/button';
import { MatInputModule } from '@angular/material/input';

import { ApiService } from '../../core/services/api-service';

@Component({
  selector: 'app-search-component',
  imports: [FormsModule, MatButtonModule, MatInputModule],
  templateUrl: './search-component.html',
  styleUrls: ['./search-component.css'],
})
export class SearchComponent {
  searchName: string = '';

  constructor(private apiService: ApiService) {}

  handleClick() {
    this.apiService.init();
  }
}
```

4. Bind the variable to the input in the `search-component.html` file.

```html
<h1>TCG Card Application</h1>

<form class="search-form">
  <mat-form-field class="search-full-width">
    <mat-label>Pokemon Name</mat-label>
    <input
      matInput
      placeholder="Ex. Dark Alakazam"
      [(ngModel)]="searchName"
      name="searchNameInput"
    />
  </mat-form-field>

  <button matButton="filled" color="primary" (click)="handleClick()">
    Search
  </button>
</form>
```

5. Now, where the `init` function is fired, let change the `handleClick` as follows.

```typescript
  async handleClick() {
    if (this.searchName.length < 5) return;

    const data = await this.apiService.queryCards(this.searchName);
    console.log(data);
  }
```

6. As a cleanup, the `init` function can be deleted from the `api-service.ts` file.

```typescript
import { Injectable } from '@angular/core';
import { CardObject } from '../interfaces/card-object';

@Injectable({
  providedIn: 'root',
})
export class ApiService {
  api: string = 'https://2026-codemash-hs-api.cloudflaretalk.com';

  generateUrl(query: string): string {
    return `${this.api}?name=${query}`;
  }

  async queryCards(query: string): Promise<Array<CardObject>> {
    const url: string = this.generateUrl(query);

    try {
      const results: any = await fetch(url, {
        method: 'GET',
        credentials: 'omit',
        headers: {
          'Content-Type': 'application/json',
        },
      });
      return await results.json();
    } catch (error) {
      console.log(error);
      return [];
    }
  }
}
```
