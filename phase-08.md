# Create and utilize a Card Component

1. Create a `shared` folder under `src`.
2. Create a `card` folder under `shared`.
3. Create the following files:

`card-component.css`

```css
.pokemon-card {
  display: inline-block;
}
.card-image {
  max-width: 100px;
}
```

`card-component.html`

```html
@if (card !== undefined) {
<mat-card class="pokemon-card" appearance="outlined">
  <mat-card-header>
    <div mat-card-avatar class="card-header-image"></div>
    <mat-card-title>{{card.name || ''}}</mat-card-title>
    <mat-card-subtitle>{{card.artist || ''}}</mat-card-subtitle>
  </mat-card-header>
  <img
    class="card-image"
    mat-card-image
    [src]="card.images.small"
    [alt]="'Photo of a ' + card.name"
  />
</mat-card>
}
```

`card-component.ts`

```typescript
import { Component, Input } from '@angular/core';
import { CardObject } from '../../core/interfaces/card-object';

import { MatCardModule } from '@angular/material/card';

@Component({
  selector: 'app-card-component',
  imports: [MatCardModule],
  templateUrl: './card-component.html',
  styleUrls: ['./card-component.css'],
})
export class CardComponent {
  @Input() card?: CardObject;
}
```

Back in the `search-component.ts` add the following code to use the card data pulled.

```typescript
import { Component } from '@angular/core';

import { FormsModule } from '@angular/forms';
import { MatButtonModule } from '@angular/material/button';
import { MatInputModule } from '@angular/material/input';

import { ApiService } from '../../core/services/api-service';
import { CardObject } from '../../core/interfaces/card-object';

import { CardComponent } from '../../shared/card/card-component';

@Component({
  selector: 'app-search-component',
  imports: [CardComponent, FormsModule, MatButtonModule, MatInputModule],
  templateUrl: './search-component.html',
  styleUrls: ['./search-component.css'],
})
export class SearchComponent {
  searchName: string = '';
  cards: Array<CardObject> = [];

  constructor(private apiService: ApiService) {}

  async handleClick() {
    if (this.searchName.length < 5) return;

    const data = await this.apiService.queryCards(this.searchName);
    this.cards = data;
  }
}
```

And, the following needs adjustment in the `search-component.html` file.

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

@if (cards.length === 0) {
<p>No records.</p>
} @else {
<div class="card-wrapper">
  @for (card of cards; track card.id) {
  <app-card-component [card]="card"></app-card-component>
  }
</div>
}
```
