# Skill: Stock Analysis

Perform comprehensive stock or portfolio analysis using YFinance data and write results to the dashboard.

---

## Task

**Goal:** Analyze individual stocks or the full portfolio, produce actionable insights, and save a structured report to `data/analysis/`.

### Steps

1. **Gather Data** — Use YFinance tools to collect:
   - Current price and fundamentals (`get_stock_fundamentals`)
   - Key financial ratios (`get_key_financial_ratios`)
   - Income statements (`get_income_statements`)
   - Analyst recommendations (`get_analyst_recommendations`)
   - Recent news (`get_company_news`)
   - Technical indicators (`get_technical_indicators`)
   - Historical prices (`get_historical_stock_prices`)

2. **Analyze** — Evaluate the stock across these dimensions:
   - **Valuation**: P/E, P/B, PEG ratio vs sector averages
   - **Growth**: Revenue and earnings growth trends
   - **Profitability**: Margins, ROE, ROA
   - **Analyst Sentiment**: Buy/hold/sell distribution and price targets
   - **Technical**: Moving averages, RSI, MACD signals
   - **News Sentiment**: Key recent developments and their likely impact
   - **Risk Assessment**: Volatility, beta, debt levels

3. **Synthesize** — Produce a clear summary with:
   - Overall outlook (Bullish / Neutral / Bearish) with confidence level
   - Key strengths and concerns (3-5 each)
   - Actionable recommendation
   - If portfolio analysis: diversification assessment, sector exposure, risk profile

4. **Save Report** — Write the analysis to `data/analysis/YYYY-MM-DD_<topic>.json`:
   ```json
   {
     "title": "Analysis title",
     "date": "YYYY-MM-DD",
     "type": "stock_analysis | portfolio_review | sector_analysis | comparison",
     "content": "Full markdown-formatted analysis"
   }
   ```

5. **Update Portfolio** — If analysis reveals updated prices, refresh `data/portfolio.json` with current prices.

### Rules

- Always use real data from YFinance. Never fabricate numbers.
- Include specific numbers and percentages, not vague statements.
- Compare metrics to industry/sector averages when possible.
- Flag any data that couldn't be retrieved rather than guessing.
- For portfolio reviews, assess correlation and diversification.
- Date all reports and reference the data retrieval time.
