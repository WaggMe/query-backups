-- Solana SPL $BONK Transactions - Last 14 Days
-- https://dune.com/queries/1832993/3015147

/* Get a tx based on id */
SELECT
  DATE_TRUNC('hour', block_time),
  COUNT(
    CASE
      WHEN CONTAINS(
        account_keys,
        'DezXAZ8z7PnrnRJjz3wXBoRgixCa6xjnB7YaB1pPB263'
      ) THEN id
      ELSE NULL
    END
  ) AS bonk
FROM
  solana.transactions
  /* exclude vote transactions */
WHERE
  block_time > (NOW() - INTERVAL '14' day)
  AND CONTAINS(
    account_keys,
    'Vote111111111111111111111111111111111111111'
  ) = FALSE
GROUP BY
  1
