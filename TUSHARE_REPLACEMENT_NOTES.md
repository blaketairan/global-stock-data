# Tushare Replacement Notes

This file records which failed or unstable data points can be replaced by Tushare and which should remain on their original sources.

## Replaced Or Added As Tushare Fallback

| Capability | Tushare API | Status |
|---|---|---|
| US daily K-line | `us_daily` | Verified with `AAPL`, returned real OHLCV rows. |
| HK daily K-line | `hk_daily` | Verified with `00700.HK`, returned real OHLCV rows. Note: current token is rate-limited to 1 request/minute for this API. |
| US stock basic info | `us_basic` | Verified with `AAPL`. |
| HK stock basic info | `hk_basic` | Verified with `00700.HK`. |
| US statements | `us_income`, `us_balancesheet`, `us_cashflow` | Verified with `AAPL`; rows are itemized by `ind_name`/`ind_value`. |
| HK statements | `hk_income`, `hk_balancesheet`, `hk_cashflow` | Verified with `00700.HK`; rows are itemized by `ind_name`/`ind_value`. |
| US key indicators | `us_fina_indicator` | Verified with `AAPL`. |
| HK key indicators | `hk_fina_indicator` | Verified with `00700.HK`. |

## Not Replaced By Tushare

| Capability | Reason |
|---|---|
| SEC Filing list | SEC EDGAR already works and is the authoritative source. |
| SEC XBRL company facts | SEC EDGAR already works and is more complete for US filings. |
| Yahoo-style analyst estimates | Tushare replacement was not confirmed for equivalent EPS estimate, rating trend, and upgrade/downgrade history coverage. |
| Yahoo-style institutional holders | Tushare replacement was not confirmed for equivalent top institutional holders and insider percentages. |
| Yahoo Finance news search | Tushare is not an equivalent news search replacement in the current skill scope. |
| Yahoo US options chain | Tushare replacement was not confirmed for US single-stock option chains with calls, puts, expirations, and Greeks. |
| HK options | The original skill already marks this as unavailable through Yahoo; Tushare was not confirmed as an equivalent HK options source. |
| US/HK fund flow | Tushare replacement was not confirmed for the Eastmoney-style main/big/mid/small order fund-flow fields. |

## Operational Notes

- Do not commit the token. The code reads `TUSHARE_TOKEN` from the environment.
- In this environment the token was found only after sourcing shell config, so non-interactive shells may need `source ~/.zshrc` or an exported process environment.
- Tushare HK daily and financial APIs returned `40203` after repeated validation calls, indicating the current token has strict frequency/day limits. The API responses have reported both minute-level and hour/day-level limits depending on endpoint.
