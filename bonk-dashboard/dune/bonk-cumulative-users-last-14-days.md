-- Solana BONK Cumulative Users - Last 14 Days
-- https://dune.com/queries/1833130/3015331
-- forked from https://dune.com/queries/625827/1167062

with user_first_ts as 
(
    select     
        account_keys[0] as wallet,
        min(date_trunc('day', block_time)) as first_seen
    from solana.transactions
    where block_time is not null
    and array_contains(account_keys, 'DezXAZ8z7PnrnRJjz3wXBoRgixCa6xjnB7YaB1pPB263')
    and block_time >= date_trunc('day', now() - interval '14 days') 
    and block_time <  date_trunc('day', now())
    group by 1
) 
select 
  first_seen as day,
  sum(count(distinct wallet)) over (order by first_seen) as cumulative_wallets
from user_first_ts
group by 1;
