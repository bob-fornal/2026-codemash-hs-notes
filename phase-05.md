# Phase 5: Create an API Service

What we will eventially be doing is searching cards.

Here is the documentation: [Search Cards](https://docs.pokemontcg.io/api-reference/cards/search-cards)

## Creating the basic service

1. Create a folder under `src` called `core`.
2. Create a folder called `interfaces` in core.
3. Add a file `card-objects.ts` in the interfaces folder.

Here's what the `card-objects.ts` file should look like.

```typescript
export interface CardObject {
  id: string;
  name: string;
  supertype: string;
  subtypes: Array<string>;
  level: string;
  hp: string;
  types: Array<string>;
  evolvesFrom: string;
  evolvesTo: string;
  rules: Array<string>;
  ancientTrait: {
    name: string;
    text: string;
  };
  abilities: Array<{
    name: string;
    text: string;
    type: string;
  }>;
  attacks: Array<{
    cost: Array<string>;
    name: string;
    text: string;
    damage: string;
    convertedEnergyCost: number;
  }>;
  weaknesses: Array<{
    type: string;
    value: string;
  }>;
  resistances: Array<{
    type: string;
    value: string;
  }>;
  retreatCost: Array<string>;
  convertedRetreatCost: number;
  set: Array<SetObject>;
  number: string;
  artist: string;
  rarity: string;
  flavorText: string;
  nationalPokedexNumbers: Array<number>;
  legalities: Array<{
    standard: string;
    expanded: string;
    unlimited: string;
  }>;
  regulationMark: string;
  images: {
    small: string;
    large: string;
  };
  tcgplayer: Array<{
    url: string;
    updatedAt: string;
    prices: Array<{
      low: number;
      mid: number;
      high: number;
      market: number;
      directLow: number;
    }>;
  }>;
  cardmarket: Array<{
    url: string;
    updatedAt: string;
    prices: Array<{
      averageSellPrices: number;
      lowPrice: number;
      trendPrice: number;
      germanProLow: number;
      suggestPrice: number;
      reverseHoloSell: number;
      reverseHoloLow: number;
      reverseHoloTrend: number;
      lowProceExPlus: number;
      avg1: number;
      avg7: number;
      avg30: number;
      reverseHoloAvg1: number;
      reverseHoloAvg7: number;
      reverseHoloAvg30: number;
    }>;
  }>;
}

export interface SetObject {
  id: string;
  name: string;
  series: string;
  printedTotal: number;
  total: number;
  legalities: Array<{
    standard: string;
    expanded: string;
    unlimited: string;
  }>;
  ptcgoCode: string;
  releaseDate: string;
  updatedAt: string;
  images: Array<{
    symbol: string;
    logo: string;
  }>;
}
```

4. Create a folder under `src/core` called `services`.
5. Create a file `api-service.ts`.

Here's what the `api-service.ts` file should look like.

```typescript
import { Injectable } from '@angular/core';
import { CardObject } from '../interfaces/card-object';

@Injectable({
  providedIn: 'root',
})
export class ApiService {
  api: string = 'https://2026-codemash-hs-api.cloudflaretalk.com';

  async init() {
    const data = await this.queryCards('dark alakazam');
    console.log(data);
  }

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

6. In the `search-component.ts` file, add the following code.

Add import for ApiService ...

```typescript
import { ApiService } from '../../core/services/api-service';
```

Add this code.

```typescipt
  constructor(apiService: ApiService) {
    apiService.init();
  }
```

At this point, we should be able to look in the console (Dev Tools, press F12) and see that data is returned.
