# polymarket-faa-attribution-02

Quantile forecaster for the 4 markets of Polymarket's FAA outage
attribution family: at each checkpoint it reads each market's 1-minute
Yes-price history (72 h) and writes, for each of the 240 minutes after the
checkpoint, the five quantiles 0.05/0.25/0.5/0.75/0.95.

Model: per market, blend the realized volatility of the last 120 and last
360 one-minute returns (0.35/0.20, halved), spread over the horizon as
sigma * sqrt(h)^1.10 around the last price, normal quantiles clamped to
[0,1] and rounded to 6 decimals. Deterministic, stdlib only, no network.

Practice pinball loss 0.276071 vs the house baseline's 0.363589
(local scorer reproduces the house baseline exactly).
