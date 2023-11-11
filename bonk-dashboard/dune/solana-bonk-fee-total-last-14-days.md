-- Solana $BONK Fee Total - Last 14 Days
-- https://dune.com/queries/1835500/3019431

WITH STATS AS (

SELECT  SUM(fee) as total_fees,
        COUNT(fee) as txs
        
FROM solana.transactions 

WHERE block_time > now() - interval '14 days'
AND array_contains(account_keys, 'DezXAZ8z7PnrnRJjz3wXBoRgixCa6xjnB7YaB1pPB263') = true
AND success="true"
)

SELECT total_fees, txs
FROM STATS