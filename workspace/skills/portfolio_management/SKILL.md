# Skill: Portfolio Management

Track and manage the user's stock portfolio. Maintain dashboard data files so the Streamlit frontend stays in sync.

---

## Task

**Goal:** Keep `data/portfolio.json` accurate and up-to-date as the user buys, sells, adds, or removes stocks.

### Actions

#### Adding a Stock
1. Fetch current price via `get_current_stock_price(symbol)`.
2. Fetch company name via `get_company_info(symbol)`.
3. Add entry to `data/portfolio.json` with the user's shares, avg cost, commission, and purchase date.
4. Recalculate all derived fields.
5. Set `last_updated` to current timestamp.

#### Removing a Stock
1. Remove the entry from `stocks` array.
2. Set `last_updated`.

#### Updating a Position (buy more / partial sell)
1. Recalculate `shares` and `avg_cost` accordingly.
   - Buying more: new avg_cost = ((old_shares × old_avg) + (new_shares × new_price)) / total_shares
   - Selling: reduce shares, avg_cost stays the same.
2. Add the new commission to the existing commission for that position.
3. Fetch latest price and recalculate derived fields.

#### Refreshing Prices
1. Loop through all stocks, call `get_current_stock_price(symbol)` for each.
2. Update `current_price`, `total_value`, `gain_loss`, `gain_loss_pct`.
3. Set `last_updated`.

---

## Data Schema

```json
{
  "stocks": [
    {
      "symbol": "AAPL",
      "name": "Apple Inc.",
      "shares": 10,
      "avg_cost": 150.00,
      "commission": 1.50,
      "purchase_date": "2025-01-15",
      "current_price": 175.50,
      "total_value": 1755.00,
      "gain_loss": 255.00,
      "gain_loss_pct": 17.00
    }
  ],
  "last_updated": "2025-01-15 14:30:00"
}
```

### Field Definitions
- `symbol` — Ticker symbol (e.g. "AAPL")
- `name` — Full company/ETF name
- `shares` — Number of shares held (can be fractional)
- `avg_cost` — Average price per share at purchase
- `commission` — Total brokerage/transaction fees paid for this position
- `purchase_date` — Date of initial purchase (YYYY-MM-DD format). If user adds more shares later, keep the original date.
- `current_price` — Latest market price
- `total_value` — shares × current_price
- `gain_loss` — total_value − (shares × avg_cost)
- `gain_loss_pct` — (gain_loss / (shares × avg_cost)) × 100

### Rules

- Always fetch live price before writing — never use stale data.
- If a symbol is invalid or YFinance returns nothing, tell the user instead of writing bad data.
- When touching portfolio.json, update ALL stocks' current prices, not just the one being modified.
- Always confirm the action back to the user with a summary of what changed.
- Track commission separately per position. If the user doesn't mention a commission, set it to 0.
- Always ask for or record the purchase date when adding new stocks. If not provided, use today's date.
