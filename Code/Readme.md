## Code

**`Examining_Features_for_Partitioning_Strategies.Rmd`**
Examines the cross-sectional distribution of California green bond yields to identify and validate the structural features used to partition bonds for curve estimation. Produces 3D scatter plots of yields colour-coded by callability, coupon range, and tax status across the term structure, and documents the partition boundaries used in the bootstrapping application. Confirms that the three selected features generate distinct and well-separated yield clusters, while comparable separation is not observed for other bond characteristics such as credit rating, issuer sector, or use of proceeds.

**`TSB_spread_calculation.Rmd`**
Computes daily term-structure-based green bond yield spreads for California municipal green bonds (2020–2024). The script partitions bonds into nine structurally homogeneous groups based on callability, coupon range, and tax status, then fits daily B1-spline bootstrap curves within each partition. Green bond cash flows are discounted using partition-specific spot rates extracted from these fitted curves, producing a green equivalent zero-coupon yield. A corresponding reference zero-coupon yield is computed by discounting the same cash flows using rates from a cubic B3-spline fitted to U.S. Treasury par yields. The daily curve-based green bond yield spread is defined as the difference between the two equivalent zero-coupon yields, and is computed for all available bonds on each trading day.

**`Spreads_distribution_and_trend_plots.Rmd`**
Produces the spread visualisation figures reported in the paper, including daily median spread trends with interquartile bands (2020–2024), kernel density estimates of the full spread distribution, and year-by-year statistical summaries.

**`ARL.Rmd`**
Applies the machine learning-based Apriori Association Rule Learning algorithm to identify structural bond attributes statistically associated with positive and negative curve-based green bond yield spreads. Bonds are labelled by the sign of their monthly median spread, and attributes including tax status, pricing type, callability, coupon range, maturity, duration, and spread at issuance are encoded and passed to the Apriori algorithm. The script reports support, confidence, and lift metrics for first-order and higher-order association rules, and tracks the temporal stability of the strongest rules over monthly rolling windows from 2020 to 2024.

**`Anova_Test.Rmd`**
Performs one-way ANOVA tests to verify the statistical significance of ARL-identified attribute associations across four maturity-based subsamples (less than 8 years, 8–12.3 years, 12.3–17 years, and above 17 years). Tests eight structural attributes and reports p-values confirming that each attribute contributes significantly to spread variation within each maturity group.

**`Bond_ladder_10_years_bonds_with_Hybrids.Rmd`**
Constructs and evaluates tenor-based (homogeneous) green bond ladder portfolios using four ARL-screened bond groups (G1–G4). At each semiannual rebalancing date, a synthetic 10-year zero-coupon bond is purchased from the relevant screened group, with pricing based on daily fitted green yield curves. A matched Treasury ladder benchmark is constructed using bootstrapped U.S. Treasury zero rates at the same tenor. The script also constructs hybrid portfolios combining screened green bonds with the Treasury benchmark at four green allocation weights (100%, 75%, 50%, 25%). Performance metrics including cumulative returns, annualised Sharpe and Sortino ratios, and maximum drawdowns are reported annually and over the full 2020–2024 sample period.

**`Bond_Ladder_-_10_ys_Duration_and_Hybrids_.Rmd`**
Constructs and evaluates duration-targeted green bond ladder portfolios that dynamically select bond maturities at each semiannual rebalancing date to maintain overall portfolio duration within a target range of 9–11 years. Bond selection follows a cost-minimisation criterion subject to the duration constraint, using the same four ARL-screened groups. A duration-matched Treasury benchmark is constructed in parallel. The script also produces hybrid duration-targeted portfolios at the same four green allocation weights and tracks the evolution of portfolio duration over time to confirm that return differentials are not attributable to duration mismatches.
