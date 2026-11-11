# Crypto Exchanges

The common crypto-exchange vocabulary -- the trading pairs an exchange lists, their tickers, the orders placed against them and the account balances behind them -- distilled from the APIs that already exist. Part of [Schema Commons](https://github.com/api-commons/schema-commons),
published by the [API Commons](https://apicommons.org).

Built from the providers tagged Cryptocurrency, Crypto Exchange, Exchange, Cryptocurrency Exchange, Digital Assets, Crypto Trading, Bitcoin in [APIs.io](https://apis.io) that
publish their own OpenAPI. Only harvested contracts count -- nothing API Evangelist
generated. Every number below is a count of providers.

## What the market already agrees on

<!-- commons:summary -->
| Concept | Expose it | Readable schema | Core properties (share) | Collection named |
| --- | ---: | ---: | --- | --- |
| trading_pair | 46 | 41 | symbol 68% | markets 18, ticker 14, pairs 13, tickers 12 |
| exchange_order | 39 | 36 | id 86%, status 75%, order_type 72%, created_at 69%, quantity 58%, side 58%, price 56%, symbol 53% | orders 32, openorders 7, order 6, open_orders 4 |
| balance | 27 | 23 |  | balance 12, accounts 10, balances 10, assets 2 |

Cohort: 288 providers with harvested OpenAPI, 55 crosswalks. Of the providers exposing a trading_pair: 0% create, 96% list, 26% fetch, 0% update, 0% delete. Generated 2026-11-11 by build.py.
<!-- /commons:summary -->

Shares are of the providers with a readable resource schema for that concept. The
extended tier and the long tail of every concept are in [profile.yml](profile.yml).

## What the measurement shows

- Exchange orders agree on id, status, order_type, created_at, quantity, side, price and symbol -- the order is the most consistent resource in crypto, across exchanges that agree on little else. time_in_force reaches 36%.
- Trading pairs agree only on the symbol; base and quote currency are spelled base, base_asset, base_ccy or base_coin, and many exchanges return a pair as a string.
- Balances share no property at half: the currency reaches 44%, and the available and held amounts are spelled free/locked, available/hold or avail_bal/frozen_bal.

## Artifacts

- [openapi.yml](openapi.yml) -- OpenAPI 3.1 of the shared operations. No one serves it; it
  is the shape to map to. Lints clean against the
  [naming ruleset](https://github.com/api-commons/schema-commons/blob/main/ruleset/schema-commons-naming.yaml).
- [schema/](schema) -- JSON Schema 2020-12 per concept; each property carries
  `x-commons-tier`, `x-commons-share`, `x-commons-providers` and the spellings seen.
- [crosswalk/](crosswalk) -- one per provider, common name -> their name, with the harvested
  spec and operations each mapping was read from.
- [adopters.yml](adopters.yml) -- who exposes which concept, linked to their APIs.io page.
- [concepts.yml](concepts.yml) -- the only hand-written input: concepts, path segments and
  their qualifiers, aliases, reviewed exclusions, merged duplicates, and the decisions below.
- [census/](census) -- the cohort and the raw census the profile is built from.

## Decisions

These are calls, not measurements, recorded so they can be revisited as the method matures.

- The order is exchange_order, because order is used in commerce and trading; it carries the market's order vocabulary (side, order_type, quantity, price, time_in_force).
- Balances and trading pairs are counted only at providers that also expose orders, which keeps wallet and banking balances out.

## Rebuild

```bash
../schema-commons/scripts/run.sh .
```

## License

Artifacts CC BY-NC-SA 4.0 ([LICENSE](LICENSE)); code Apache 2.0 ([LICENSE-CODE](LICENSE-CODE)).
