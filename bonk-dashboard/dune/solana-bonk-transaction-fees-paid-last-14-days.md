-- Solana Bonk Transaction Fees Paid - Last 14 Days
-- https://dune.com/queries/1835429/3019368

WITH STATS AS (

SELECT  date_trunc('day',block_time) as day,
        --block_slot, 
        --fee,
        SUM(fee) as total_fees,
        COUNT(fee) as txs
        
FROM solana.transactions 

WHERE block_time > now() - interval '14 days'
AND array_contains(account_keys, 'DezXAZ8z7PnrnRJjz3wXBoRgixCa6xjnB7YaB1pPB263') = true
AND success="true"

GROUP BY day
)

SELECT total_fees, day
FROM STATS

ORDER BY day DESC