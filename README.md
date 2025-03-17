# ETH Price Movement Analysis Across Uniswap V3 Fee Tiers

This repository contains the analysis and methodology for investigating how ETH price movements propagate across different Uniswap V3 fee tiers.

## Overview

Uniswap V3 offers multiple fee tiers (1bps, 5bps, 30bps, 100bps) for liquidity providers. This research examines how price movements in a 5bps ETH-USDC pool would translate to higher fee tiers, helping to understand:

1. The trade-off between fee revenue and trading volume
2. Price tracking accuracy across different fee tiers
3. Optimal fee tier selection for different market conditions

## Methodology

Our analysis uses a novel approach based on directional price movements rather than individual transactions:

1. **Peak Detection Algorithm**
   - We identify local price maxima and minima to detect meaningful directional changes
   - A "movement" is defined as a continuous price trend between consecutive extrema
   - We apply a minimum threshold (0.03%) to filter out noise

2. **Fee Tier Simulation**
   - For each fee tier, we simulate how the ETH price would evolve
   - A price movement triggers trading activity when its percentage change exceeds the fee
   - We calculate the "effective" price change as the actual change minus the fee differential

3. **Performance Metrics**
   - Trading volume based on effective price changes
   - Fee revenue (volume × fee percentage)
   - Price tracking accuracy (deviation from the actual price path)
   - Update frequency (percentage of price points that trigger updates)

## Key Findings

1. **Fee Revenue vs Volume**
   - The 12bps tier maximizes fee revenue (~$26,024 daily)
   - Lower fee tiers capture more trading volume, but at lower fees per trade
   - Higher fee tiers capture fewer movements but generate more fee per movement

2. **Price Tracking Accuracy**
   - Lower fee tiers track the actual ETH price more accurately
   - Higher fee tiers show "stair-step" price patterns with larger deviations
   - This difference helps explain price discrepancies across pools

3. **Optimal Fee Tier**
   - For this specific dataset (24 hours of ETH-USDC trading):
     * 5bps tier: Highest volume ($40.1M), 83.0% of movements
     * 12bps tier: Highest fee revenue ($26,024), 43.2% of movements
     * 30bps tier: Lowest revenue of analyzed tiers ($15,539), 8.7% of movements

## Data

The analysis uses 6,687 swap events from a 5bps ETH-USDC pool over a 24-hour period, processed to extract:
- ETH-USD prices from sqrtPriceX96 values
- Percentage price changes
- Directional price movements


## Dependencies

- pandas
- numpy
- matplotlib
- scipy (for peak detection)

## Contributors

[Ishan]

## License

