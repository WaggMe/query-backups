-- Solana BONK DAU - Last 14 Days
-- https://dune.com/queries/1833152/3015340
-- forked from https://dune.com/queries/620299/1157620

SELECT time, count(distinct user) as active_users from (

SELECT
    account_keys[0] AS user,
    MIN(date_trunc('day', block_time)) AS time
    FROM solana.transactions

    WHERE array_contains(account_keys, 'DezXAZ8z7PnrnRJjz3wXBoRgixCa6xjnB7YaB1pPB263')
    AND success = TRUE
    AND  block_time > now() - interval '14 days'
    GROUP BY 1
)

GROUP BY 1
