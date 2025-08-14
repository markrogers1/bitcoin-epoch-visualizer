# Bitcoin Difficulty Epoch Visualizer

An interactive, mempool-style grid that visualizes **Bitcoin difficulty epochs** (2016 blocks each). As blocks are mined, cells light up and color by **time-to-mine**. Hover for detailed block info. A new grid starts automatically when the **difficulty adjusts**.

- ✅ Live data via **mempool.space** REST API (`/api/blocks` poll + per-block enrich)
- ✅ Accessibility-friendly (keyboard focus, ARIA labels, tooltips)
- ✅ No build tools required — just static HTML (perfect for GitHub Pages)
- ⚙️ Customizable columns (8–63) and epoch history (keep last 3)

## Demo (GitHub Pages)

After you publish, your site will be available at:

```
https://<your-username>.github.io/bitcoin-epoch-visualizer/
```

## How it works

- The page renders a **2016-cell grid** per epoch (default 32×63).
- Blocks are colored by **time-to-mine** between consecutive blocks:
  - Fast: ≤ 8 min
  - Normal: 8–15 min
  - Slow: > 15 min
- Hover (or focus with keyboard) to see a tooltip with height, timestamp, miner, tx count, size, weight, fees, hash.

## Run locally

Just open `index.html` in your browser. It will fetch recent blocks and poll for new ones automatically.

> Note: Using the public mempool.space API directly from the browser. If you run into CORS or rate limits on other providers, consider deploying to Pages or proxying the API.

## Deploy to GitHub Pages

1. Create a new repo, e.g. `bitcoin-epoch-visualizer`.
2. Add the files and push to `main`.
3. In **Settings → Pages**, choose **Source: Deploy from a branch**, Branch: `main`, Folder: `/root`. Save.
4. Wait for the green checkmark on Actions, then open your Pages URL.

## Customization

- **Grid columns**: change via the input in the header (8–63). Layout recalculates without losing filled cells.
- **Keep history**: toggle to keep the last 3 epochs visible; otherwise only the latest epoch shows.
- **Colors**: tweak the CSS custom properties in `:root`:
  ```css
  --fast: #24c486;
  --normal: #f0c44e;
  --slow: #e35b5b;
  --pending: #27374b;
  ```
- **Poll interval**: default is `10s`. Change in `setInterval(poll, 10000)`.

## Switching to WebSockets (optional)

If you want push updates instead of polling, you can use `@mempool/mempool.js` and subscribe to the `blocks` channel. Replace the REST section with a WS client (see mempool.space docs).

## Data source

- `GET https://mempool.space/api/blocks` — last ~15 blocks (height, id, timestamp, tx_count, size, weight)
- `GET https://mempool.space/api/block/:hash` — detailed block info (size, weight, fees, pool when available)

## License

MIT — see `LICENSE`.
