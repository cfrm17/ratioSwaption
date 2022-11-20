# Ratio Swaption Model

A single currency BMA Ratio Swap is a swap contract with two legs. The BMA leg pays the average of weekly BMA resets observed during the (BMA leg) coupon accrual period. The Libor leg pays Libor times the BMA ratio (also called the multiplier), specified in the contract. 

The holder of a BMA Receiver Swap receives the multiplier × Libor leg. The holder of a BMA Payer Swap pays the multiplier × Libor. Hence the terms ’payer’ and ’receiver’ refer to the multiplier × Libor leg. 

A BMA Ratio Swaption gives the holder the right, but not the obligation, to enter into a BMA ratio swap. The exercise style may be European or Bermudan.


Here is an example deal that was traded on the market

• Underlying swap - spot starting, 10Y maturity, the swap holder receives 75% times Libor coupon payments (see https://finpricing.com/lib/FiBondCoupon.html). 100M notional.

• Option - Bermudan exercise dates every three months. The expiry date is in 10Y.

Note in this example deal both the swap and the option start on the valuation date. On the succeeding Bermudan exercise date the underlying swap term decreases. So on the initial valuation date the underlying is a 10Y swap. On the 3M Bermudan date the underlying is a 9Y 9M ratio swap. And so on. Note - the subject model only handles payment in arrears. At the present time it does not calculate convexity adjustment for underlying ratio swaps that pay in-advance on every accrual period.

We employ the standard definition for a vanilla Libor swap. For this contract the Libor swap rate is calculated by setting the PV of the fixed and Libor legs to be the same:

 

Hence, we also define a BMA swap rate just like a Libor swap rate as follows

 

Finally, the BMA Ratio Swap has a BMA average rate leg and a leg that pays the product of Libor and the BMA Ratio ρ . The breakeven ratio is defined such that these two legs have the same value

 

The key insight of the model is to notice the following simple relationship, which is obtained by combining Equations above:

 

Hence it is possible to value a contract whose payoff is a function of the BMA ratio (which is the case of the BMA ratio swaption) by building a model for Libor and BMA swap rates.

Under money market measure (Q, MMA), we assume that BMA swap rate and Libor swap rate are following two different driftless Geometry Brownian Motions:

 


where yL and yB  are current forward Libor swap rate and current forward BMA swap rate, σL (t) andσB (t) are volatility functions. In fact, they are given by linear interpolation methods from the set of N sample points. Here {Xt } and {Zt } are independently Brownian motions and σB (t) = g(σL (t)) and g(t) is a given deterministic function of t . This is two single factors model and it is standard market practice.

The fundamental theorem for arbitrage-free valuation is




