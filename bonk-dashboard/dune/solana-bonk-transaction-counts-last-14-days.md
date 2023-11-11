-- Solana $BONK Transaction Count - Last 14 Days
-- https://dune.com/queries/1835473/3019393

/* Get a tx based on id */
SELECT
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
