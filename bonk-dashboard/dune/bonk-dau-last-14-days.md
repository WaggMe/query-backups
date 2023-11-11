-- Solana BONK DAU - Last 14 Days
-- https://dune.com/queries/1833152/3015340
-- forked from https://dune.com/queries/620299/1157620

/* forked from https://dune.com/queries/620299/1157620 */
SELECT
  time,
  COUNT(DISTINCT user) AS active_users
FROM
  (
    SELECT
      ELEMENT_AT(account_keys, 0 + 1) AS user,
      MIN(DATE_TRUNC('day', block_time)) AS time
    FROM
      solana.transactions
    WHERE
      CONTAINS(
        account_keys,
        'DezXAZ8z7PnrnRJjz3wXBoRgixCa6xjnB7YaB1pPB263'
      )
      AND success = TRUE
      AND block_time > NOW() - INTERVAL '14' day
    GROUP BY
      1
  )
GROUP BY
  1
