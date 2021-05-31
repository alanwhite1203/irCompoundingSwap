# Compounding Swap Valuation Practical Guide

Overview
A compounding swap is an interest rate swap in which interest, instead of being paid, compounds forward until the next payment date. Compounding swaps can be valued by assuming that the forward rates are realized. Normally the calculation period of a compounding swap is smaller than the payment period. For example, a swap has 6-month payment period and 1-month calculation period (or 1-month index tenor). An overnight index swap (OIS) is a typical compounding swap. This presentation gives an overview of compounding swap product and valuation model. 

	Keywords
Compounding swap, Interest rate swap, OTC derivatives, swaplet, valuation, pricing model, interest rate risk

	Compounding Swap Introduction
	A compounding swap is an interest rate swap in which interest, instead of being paid, compounds forward until the next payment date.
	Compounding swaps can be valued using the rule of assuming that the forward rate is realized.
	Normally the calculation period of a compounding swap is smaller than the payment period. For example, a swap has 6-month payment frequency and 1-month calculation period (or 1-month index tenor).
	An overnight index swap (OIS) is a typical compounding swap.

	Compounding Swap or Compounding Swaplet Payoff
	Assuming that An average compounded swap consists of two legs: a regular fixed leg and a compounding floating leg.
	The compounding leg is similar to a regular floating leg except the reset frequency is higher than the payment frequency. For example, a compounding leg has 1 month reset frequency and 6 month payment frequency.
	From the fixed rate payer perspective, the payoff of a swap or swaplet at payment date T is given by
〖Payff〗_payer=NτR-NF)
where 
N- the notional;
 τ – accrual period in years (e.g., a 3 month period ≈ 3/12 = 0.25)
R – the fixed rate in simply compounding.
F=∏_(j=1)^k▒〖(1+Q_j )-1〗 – the realized compounded floating rate for a payment period, e.g., 6-month
Q_j=r_j τ_j – the accrued interest for a calculation period, say, 1-month
	From the fixed rate receiver perspective, the payoff of a swap or swaplet at payment date T is given by
〖Payff〗_receiver=Nτ(F-R)

	Valuation
	The present value of a fixed rate leg is given by

〖PV〗_fixed (t)=RN∑_(i=1)^n▒〖τ_i D_i 〗
where t is the valuation date and D_i=D(t,T_i) is the discount factor.
	The present value of a floating leg is given by
〖PV〗_compound (t)=N∑_(i=1)^n▒〖(∏_(j=1)^k▒〖(1+Q_i 〗)-1) τ_i D_i 〗
where
Q_j=〖(r〗_(j+s)) τ_j –the accrued interest for calculation period j.
 F_i=(D_(i-1)/D_i -1)/τ_i - the simply compounded forward rate
s - the floating spread.
	The present value of an interest rate swap can expressed as
	From the fixed rate payer perspective, PV=〖PV〗_float-〖PV〗_fixed		
	From the fixed rate receiver perspective, PV=〖PV〗_fixed-〖PV〗_float

	Practical Notes
	First of all, you need to generate accurate cash flows for each leg. The cash flow generation is based on the start time, end time and payment frequency of the leg, plus calendar (holidays), business convention (e.g., modified following, following, etc.) and whether sticky month end.
	We assume that accrual periods are the same as reset periods and payment dates are the same as accrual end dates in the above formulas for brevity. But in fact, they are different due to different market conventions. For example, index periods can overlap each other but swap cash flows are not allowed to overlap.
	The accrual period is calculated according to the start date and end date of a cash flow plus day count convention 
	The forward rate should be computed based on the reset period (index reset date, index start date, index end date)  that are determined by index definition, such as index tenor and convention. it is simply compounded.
	Sometimes there is a floating spread added on the top of the floating rate in the floating leg.
	The formula above doesn’t contain the last live reset cash flow whose reset date is less than valuation date but payment date is greater than valuation date. The reset value is
〖PV〗_reset=r_0 Nτ_0 D_0  
where r_0 is the reset rate. 
	The present value of the reset cash flow should be added into the present value of the floating leg.
	Some dealers take bid-offer spreads into account. In this case, one should use bid curve constructed from bid quotes for forwarding and offer curve built from offer quotes for discounting.

	A Real World Example
Leg 1 Specification	Leg 2 Specification
Currency	USD	Currency	USD
Day Count	dcAct360	Day Count	dcAct360
Leg Type	Fixed	Leg Type	Float
Notional	5000000	Notional	5000000
Pay Receive	Receive	Pay Receive	Pay
Payment Frequency	6M	Payment Frequency	6M
Start Date	7/1/2015	Start Date	7/1/2015
End Date	3/1/2023	End Date	3/1/2023
Fixed Rate	0.0455	Spread	0
		Index Specification
		Index Type	LIBOR
		Index Tenor	1M
		Index Day Count	dcAct360


References:

https://finpricing.com/lib/EqVariance.html

https://bitbucket.org/cmrm11/ircompoundingswap/downloads/IrCompoundingSwap-32.pdf


