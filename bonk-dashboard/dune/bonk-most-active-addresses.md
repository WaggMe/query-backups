-- BONK Most Active Addresses
-- https://dune.com/queries/1839468/3025923

/* Query done by @ennnas */
/* Original Query link: https://dune.com/queries/1839175 */
SELECT
  token_balance_owner,
  CASE
    WHEN token_balance_owner = '5P6n5omLbLbP4kaPGL8etqQAHEx2UCkaUyvjLDnwV4EY' THEN 'Orca Bonk/USDC'
    WHEN token_balance_owner = 'BqnpCdDLPV2pFdAaLnVidmn3G93RP2p5oRdGEY2sJGez' THEN 'Orca Sol/Bonk'
    WHEN token_balance_owner = '9gd6zAAtP1wdaV9NcxTyvmCPVE8HycPWCA2jPF6GgpX6' THEN 'Orca USDH/Bonk'
    WHEN token_balance_owner = 'A9yRKSx8SyqNdCtCMUgr6wDXUs1JmVFkVno6FcscSD6m' THEN 'Openbook Bonk/USDC'
    WHEN token_balance_owner = '5Q544fKrFoe6tsEbD7S8EmxGTJYAKtTVhAW5Q5pge4j1' THEN 'Raydium Bonk/USDC'
    WHEN token_balance_owner = '2PFvRYt5h88ePdQXBrH3dyFmQqJHTNZYLztE847dHWYz' THEN 'Saros Bonk/USDC'
    ELSE 'Unknown'
  END AS account_label,
  SUM(ABS(token_balance_change)) AS volume_traded
FROM
  solana.account_activity
WHERE
  block_time > (NOW() - INTERVAL '1' day)
  AND token_mint_address = 'DezXAZ8z7PnrnRJjz3wXBoRgixCa6xjnB7YaB1pPB263'
  AND token_balance_owner IN (
  '5P6n5omLbLbP4kaPGL8etqQAHEx2UCkaUyvjLDnwV4EY',
  'BqnpCdDLPV2pFdAaLnVidmn3G93RP2p5oRdGEY2sJGez',
  '9gd6zAAtP1wdaV9NcxTyvmCPVE8HycPWCA2jPF6GgpX6',
  'A9yRKSx8SyqNdCtCMUgr6wDXUs1JmVFkVno6FcscSD6m',
  '5Q544fKrFoe6tsEbD7S8EmxGTJYAKtTVhAW5Q5pge4j1',
  '2PFvRYt5h88ePdQXBrH3dyFmQqJHTNZYLztE847dHWYz'
  )
GROUP BY
  token_balance_owner
ORDER BY
  volume_traded DESC
