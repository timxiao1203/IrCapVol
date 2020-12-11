# Ir Cap Implied Volatility Surface

Overview
	An implied volatility is the volatility implied by the market price of an option based on the Black-Scholes option pricing model. In cap market, a cap/floor is quoted by implied volatilities but not prices. An interest rate cap volatility surface is a three-dimensional plot of the implied volatility of a cap as a function of strike and maturity. 
	The term structures of implied volatilities which provide indications of the market’s near- and long-term uncertainty about future short- and long-term forward interest rates. A crucial property of the implied volatility surface is the absence of arbitrage.

Summary
	Cap Volatility Surface Introduction
	The Summary of Volatility Surface Construction Approaches
	Arbitrage Free Conditions
	The SABR Model
	Cap Volatility Surface Construction via The SABR Model

Cap Volatility Surface Introduction
	An implied volatility is the volatility implied by the market price of an option based on the Black-Scholes option pricing model. 
	In market, a cap/floor is quoted by implied volatilities rather than prices.
	An interest rate cap volatility surface is a three-dimensional plot of the implied volatility of a cap as a function of strike and maturity. 
	The term structures of implied volatilities provide indications of the market’s near- and long-term uncertainty about future short- and long-term forward rates.
	Vol skew or smile pattern is directly related to the conditional non-normality of the underlying returns. In particular, a smile reflects fat tails in the return distribution whereas a skew indicates asymmetry.
	A crucial property of the implied volatility surface is the absence of arbitrage.

The Summary of Volatility Surface 
Construction Approaches
	To construct a reliable volatility surface, it is necessarily to apply robust interpolation methods to a set of discrete volatility data. Arbitrage free conditions may be implicitly or explicitly embedded in the procedure. Typical approaches are
	Local Volatility Model: a generalisation of the Blaack-Scholes model.
	Stochastic Volatility Models: such as SABR, Heston, Levy
	Parametric or Semi-Parametric Models: such as SVI, Omega
	Market Volatility Model: directly modeling the implied volatility dynamics
	Interpolation/Extrapolation Model: interpolating or extrapolating volatility data using specific function forms

Arbitrage Free Conditions
	Any volatility models must meet arbitrage free conditions.
	Typical arbitrage free conditions
	Static arbitrage free condition: Static arbitrage free condition makes it impossible to invest nothing today and receive positive return tomorrow. 
	Calendar arbitrage free condition: The cost of a calendar spread should be positive.
	Vertical (spread) arbitrage free condition: The cost of a vertical spread should be positive.
	Horizontal (butterfly) arbitrage free condition: The cost of a butterfly spread should be positive.
	Vertical arbitrage free and horizontal arbitrage free conditions for cap volatility surfaces are based on different strikes
	There is no calendar arbitrage in cap volatility surfaces as caps with different maturities have different cash flows and are associated with different indices. In other words, they can be treated independently.
	At FinPricing, we use the SABR model to construct cap volatility surfaces following the best market practice.

The SABR Model
	SABR stands for “stochastic alpha, beta, rho” referring to the parameters of the model.
	The SABR model is a stochastic volatility model for the evolution of the forward price of an asset, which attempts to capture the volatility smile/skew in derivative markets.
	There is a closed-form approximation of the implied volatility of the SABR model.
	In the cap volatility case, the underlying asset is the forward interest rate.
	The dynamics of the SABR model
dF ̂=α ̂F ̂^β dW_1
dα ̂=vα ̂dW_2
dW_1 dW_2=ρdt
α ̂(0)=α
where
		F ̂	the forward swap rate
		α ̂	the forward volatility
W_1,W_2	the standard Brownian motions
ρ	the instantaneous correlation between W_1  and W_2
	The four model parameters (a , b , r, n ) above have the following intuitive meaning:
	𝛼		the volatility that is tied closely to the at-the-money volatility value.
	𝛽 	the exponent that is related to the backbone that the ATM volatility traces when the ATM forward rate varies.
	𝜌 	the correlation that describes the “skew” or average slope of the volatility curve across strike.
	𝑣 	the volatility of volatility that describes the “smile” or curvature/convexity of the volatility curve across the strike for a given term and tenor.

Constructing Cap Volatility Surface 
via The SABR Model
	For each maturity of a cap/floor, conduct the following calibration procedure.
	The 𝛽 parameter is estimated first and typically chosen a priri according to how the market prices are to be observed.
	Alternatively 𝛽  can be estimated by a linear regression on a time series of ATM volatilities and of forward rates.
	After 𝛽 is set, we can obtain 𝛼 by using  𝜎﷮𝐴𝑇𝑀﷯ to solve the following equition
	σ_ATM=α/f^(1-β)  {1+[(α^2 〖(1-β)〗^2)/(24f^(2(1-β)) )+ρβvα/(4f^(1-β) )+((2-3ρ^2)v^2)/24]T}
The Viete method is used to solve this equation

Constructing Cap Volatility Surface 
via The SABR Model
	Given the 𝛼 and 𝛽  solved above,  we can find  the optimized  value  of (𝜌,𝑣) by minimizing the distance between the SABR model output volatilities and market volatilities across all strikes for each term and tenor.
	min∑_(i=1)^n▒[σ_i^SABR (α,β,ρ,v)-σ_i^Market ]^2 
The Levenberg-Marquardt least-squares optimization routine is used for optimization.
	After 𝛼,𝛽,𝜌,𝑣 calibrated, one can generate SABR volatility (cap volatility) for any moneyness.
	Repeat the above process for each term and tenor.


You can find more details at
https://finpricing.com/lib/FxVolIntroduction.html
