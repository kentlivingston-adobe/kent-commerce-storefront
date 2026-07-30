# Promo Banner Block

## Overview

The Promo Banner block displays a heading and a grid of featured products pulled from a specific category via Catalog Service (Live Search) GraphQL. Each product links to its PDP and shows its image, name, and price.

## Integration

### Block Configuration

Read via `readBlockConfig()`:

- `category-id` — category ID to source products from (required for results; empty string returns no products)
- `heading` — heading text displayed above the product grid (default: `Featured Products`)
- `max-products` — maximum number of products to display (default: `4`)

### URL Parameters

No URL parameters directly affect this block's behavior.

### Local Storage

No localStorage keys are used by this block.

### Events

#### Event Listeners

No direct event listeners are implemented in this block.

#### Event Emitters

No events are emitted by this block.

## Behavior Patterns

### Data Fetching

- On decoration, the block queries Catalog Service (`CS_FETCH_GRAPHQL`) via `productSearch`, filtering by `category-id` and limited to `max-products` results.
- Product links are built with `getProductLink(urlKey, sku)`, resolving to `/products/{urlKey}/{sku}`.

### User Interaction Flows

1. **Initialization**: Block renders a heading and a "Loading products..." placeholder.
2. **Data Display**: Once the query resolves, the products container is replaced with a grid of linked product cards (image, name, price).
3. **Empty Results**: If no products are returned, displays "No products found."

### Error Handling

- **Query Errors**: If the GraphQL request fails, the error is logged to the console and "Unable to load products." is shown in place of the product grid.
- **Missing Image/Price**: Product cards render without an image or price if either is absent from the response.
