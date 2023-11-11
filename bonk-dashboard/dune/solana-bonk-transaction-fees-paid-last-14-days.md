-- Solana Bonk Transaction Fees Paid - Last 14 Days
-- https://dune.com/queries/1835429/3019368

WITH
  STATS AS (
    SELECT
      DATE_TRUNC('day', block_time) AS day,
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
    GROUP BY
      1
  )
SELECT
  total_fees,
  day
FROM
  STATS
ORDER BY
  day DESC
WITH
  STATS AS (
    SELECT
      DATE_TRUNC('day', block_time) AS day,
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
    GROUP BY
      1
  )
SELECT
  total_fees,
  day
FROM
  STATS
ORDER BY
  day DESC
