-- BONK Top 1k Holders
-- https://dune.com/queries/1838819/3024923

/* Query done by @ennnas */
/* Original query link: https://dune.com/queries/1837273 */
SELECT DISTINCT
  item.owner,
  FIRST_VALUE(item.amount) OVER (
    PARTITION BY
      item.account
    ORDER BY
      block_slot DESC
  ) AS token_balance
FROM
  (
    SELECT
      block_slot,
      post_token_balances
    FROM
      solana.transactions
    WHERE
      block_date > CAST('2022-12-08' AS DATE) /* Date when BONK was first created */
      AND CONTAINS(
        account_keys,
        'Vote111111111111111111111111111111111111111'
      ) = FALSE /* exclude voting transactions to make the query faster */
      AND CONTAINS(
        account_keys,
        'DezXAZ8z7PnrnRJjz3wXBoRgixCa6xjnB7YaB1pPB263' /* bonk mint address */
      ) = TRUE
      AND success = TRUE
  )
  CROSS JOIN UNNEST (post_token_balances) AS item
WHERE
  item.mint = 'DezXAZ8z7PnrnRJjz3wXBoRgixCa6xjnB7YaB1pPB263'
ORDER BY
  token_balance DESC
LIMIT
  1000
