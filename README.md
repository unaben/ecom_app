# Clothing store

Live: dynamic-ecomm-app.netlify.app

A small e-commerce front end in React and TypeScript. You can browse products, pick a colour and size, search, fill a cart and click through a checkout. There's no backend, so no orders are really placed.

## What's in it

- **Store page:** products filtered by gender (men, women, unisex), with the choice kept in the URL (`?gender=`) so links and the back button behave.
- **Product pages:** colour and size selectors, quantity, stock status per variant, and related products.
- **Search:** a modal with suggestions and recent searches, plus a full results page with filter chips, category and price filters, and sorting.
- **Cart:** a slide-out cart where you can change quantities or remove items. Adding the same variant twice merges the lines.
- **Checkout:** contact, delivery, shipping and payment sections with an order summary, ending on a confirmation page. It's all front end; nothing is sent anywhere.

## How it's put together

Products come from a static file, `public/products.json`. `fetchProducts` loads it and works out stock for each product from its variants, and TanStack Query handles caching (5 minute stale time, 2 retries). Routing lives in one place, `buildRoutes`, which turns the app state into each route's props.

Each component has its own folder with its styles and types, and bigger ones split their pieces into `components/`, `utils/` and `hooks/` folders. The search results filtering and sorting are small pure functions in `SearchResults/utils`, which keeps them easy to test.

## Running it

Needs Node 18 (there's an `.nvmrc`).

```bash
nvm use
npm install
npm start
```

Then open http://localhost:3000. `npm run build` makes a production build.

## Rough edges

- The only test is the default Create React App one, which still looks for the "learn react" link, so it fails. Real tests are on my list, starting with the search utils and cart logic.
- Prices in the cart are stored as line totals rather than unit prices, which makes quantity changes fiddlier than they should be.
- Create React App is no longer maintained. If I kept going I'd move this to Vite.

## Stack

React 18, TypeScript, React Router 6, TanStack Query 5, CSS Modules, classnames.
