# GoodFind

GoodFind is a responsive product-discovery page built with **vanilla HTML, CSS, and JavaScript**. It loads a product catalogue from the DummyJSON Products API and lets people search, filter, sort, and recover easily when there are no matches.

## Features

- Live search across product title, brand, and category.
- Category filter populated from the API response.
- Minimum and maximum price filters that can be combined with search and category.
- Sorting by featured order, price (low-to-high / high-to-low), and rating.
- Result count and a helpful empty state with a one-click reset.
- Loading state, API error state, and retry action.
- Responsive layout with a collapsible filter panel on small screens.
- Keyboard shortcut to focus search: `Ctrl + K` on Windows/Linux and `⌘ + K` on macOS. Press `Escape` while the search field is focused to clear the query.
- Accessible labels, visible keyboard focus, live result announcements, lazy-loaded product images, and image fallbacks.

## Run locally

No build step or package installation is required.

1. Download or clone this repository.
2. Open `index.html` in a browser, or use the VS Code **Live Server** extension.
3. An internet connection is required because the product data and images come from DummyJSON.

## How the filtering works

The page applies all active criteria together:

1. Search query (title, brand, or category)
2. Selected category
3. Minimum price, if provided
4. Maximum price, if provided
5. Selected sort order

Filtering and sorting are kept in `matchingProducts()` so that every control uses the same result pipeline. `render()` updates the result count and grid, and shows the empty state when no products match. The reset action clears the search, category, price bounds, and sort selection together.

## Design and implementation choices

- **Vanilla JavaScript:** keeps the project lightweight and avoids a build tool or framework requirement.
- **Single HTML file:** HTML, CSS, and JavaScript are together for easy review and simple deployment. For a larger product, these would be split into separate files/modules.
- **Client-side filtering:** the catalogue is fetched once, then filters and sorting run locally for immediate feedback.
- **Responsive CSS grid:** uses breakpoints to adapt the catalogue and turns the filter panel into a disclosure on mobile.
- **DOM-created product cards:** product text is inserted with `textContent` rather than interpolating API text into HTML, reducing injection risk.
- **Graceful failure:** failed API requests show a retry action instead of leaving the page stuck on the loading state.

## Trade-offs and limitations

- The product catalogue is a public demo API, not a production inventory service; availability and data may change.
- Prices are displayed in USD to match the API/demo presentation. Currency conversion is not implemented.
- Search and filters operate on the products returned by the API; there is no server-side pagination or persistent saved state.
- The design focuses on discovery rather than checkout, authentication, or product-detail pages.
- The `Featured` sort preserves the order returned by the API; it is not a custom recommendation algorithm.

## Manual test checklist

- [ ] Search by a word in a product title.
- [ ] Search by a brand and by a category name.
- [ ] Select a category while a search query is active.
- [ ] Apply minimum and maximum prices while search/category filters are active.
- [ ] Sort the filtered results by both price directions and rating.
- [ ] Enter a range where minimum is greater than maximum; confirm the hint explains the issue and no results are shown.
- [ ] Search for an impossible term; confirm the empty state appears.
- [ ] Use **Clear search & filters** and confirm all controls reset.
- [ ] Use `Ctrl + K` / `⌘ + K` to focus search, and `Escape` to clear the query.
- [ ] Test at mobile width and desktop width.
- [ ] Disconnect the network and reload; confirm the retry state appears.

## Data source

- [DummyJSON Products API](https://dummyjson.com/docs/products)

## License

Add a license if you intend to distribute or reuse this project publicly.
