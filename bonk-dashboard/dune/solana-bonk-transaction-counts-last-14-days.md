-- Solana $BONK Transaction Count - Last 14 Days
-- https://dune.com/queries/1835473/3019393

-- Get a tx based on id
select
    count(case when array_contains(account_keys, 'DezXAZ8z7PnrnRJjz3wXBoRgixCa6xjnB7YaB1pPB263') then id else null end) bonk

from solana.transactions
-- exclude vote transactions
where block_time > (NOW() - interval '14 days')
and array_contains(account_keys, 'Vote111111111111111111111111111111111111111') = false
