-- Solana $BONK Fee Total - Last 14 Days
-- https://dune.com/queries/1835500/3019431

WITH
  STATS AS (
    SELECT
      SUM(fee) AS total_fees,
      COUNT(fee) AS txs
    FROM
      solana.transactions
    WHERE
      block_time > NOW() - INTERVAL '14' day
      AND CONTAINS(
        account_keys,
        'DezXAZ8z7PnrnRJjz3wXBoRgixCa6xjnB7YaB1pPB263'
      ) = TRUE
      AND success = TRUE
  )
SELECT
  total_fees,
  txs
FROM
  STATS
