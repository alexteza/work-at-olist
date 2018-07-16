# Database Modelling I
This is the most complete modelling to solve this chalenge.
This modelling gives some positive and negative points:
### Positive:
 - Configurable Pricing rules gives flexibiliti to create promotion periods.
 - Configurable Pricing rules gives flexibiliti to adjust the price during the campaing at a single place.
### Negative:
 - Grow the complexity of implementation.
 - Needs a posprocess to atach the correct Pricing rules to call or a extra query to get it, that make the process more slow.

## PricingRules
|Fields|Example rule|
|--|--|
|ID|1|
|PeriodStat|2018-01-01T00:00:00+00:00|
|PeriodEnd|2018-01-01T23:59:59+00:00|
|StartBillingTime|06:00|
|EndBillingTime|22:00|
|StandingCharge|0.36|
|CallCharge|0.09|
  
## Calls
|Fields|Example call|
|--|--|
|ID|c36acc8a-088f-4043-ac28-4b1342409a0b|
|Source|41991954421|
|Destination|41996754421|
|PricingRule|1|

## Details
|Fields|Example detail start|Example detail end|
|--|--|--|
|ID|18f10cd9-2530-4174-abb4-60cbf3829f1f|83cd046a-0140-4dfd-9522-17462a3d9fa0|
|Call|c36acc8a-088f-4043-ac28-4b1342409a0b|c36acc8a-088f-4043-ac28-4b1342409a0b|
|Type|1|2|
|Timestamp|2018-01-01T10:00:00+00:00|2018-01-01T00:10:30+00:00|

> * Details Type: 1 = Start call; 2 = End call.

# Database Modelling II
This is a variation from "Database Modelling I" taking off the PricingRules table and transfering this responsability to system configuration or to the initialization parameters.
This modelling gives some positive and negative points:
### Positive:
 - Reduces the complexity of implementation.
 - Brings the pricing rules to the “call end” without the posprocess or extra queries to do this, making the process more fast.
### Negative:
 - If you need to adjust the price during the campaing it just can be made by reconfiguring the system and updating all the calls finiched during this period.

## Calls
|Fields|Example call|
|--|--|
|ID|c36acc8a-088f-4043-ac28-4b1342409a0b|
|Source|41991954421|
|Destination|41996754421|
|StandingCharge|0.36|
|CallCharge|0.09|

## Details
|Fields|Example detail start|Example detail end|
|--|--|--|
|ID|18f10cd9-2530-4174-abb4-60cbf3829f1f|83cd046a-0140-4dfd-9522-17462a3d9fa0|
|Call|c36acc8a-088f-4043-ac28-4b1342409a0b|c36acc8a-088f-4043-ac28-4b1342409a0b|
|Type|1|2|
|Timestamp|2018-01-01T10:00:00+00:00|2018-01-01T00:10:30+00:00|

> * Details Type: 1 = Start call; 2 = End call.

# Database Modelling III
This is a variation from "Database Modelling I" taking off the PricingRules table, transfering this responsability to system configuration or to the initialization parameters and taking off the Details table, transfering this data to the Call table.
This is the most clean and simple implementation modellig, but have some positive and negative points too:
### Positive:
 - Dramatically reduces the complexity of implementation.
 - Brings the pricing rules to the “call end” without the posprocess or extra queries to do this, making the process more fast.
### Negative:
 - If you need to adjust the price during the campaing it just can be made by reconfiguring the system and updating all the calls finiched during this period.
 - Obsviously we need to update the data to finish every calls, turning imposible the use of imutable databases, which would be my recommendation for this type of system.

## Calls
|Fields|Example call|
|--|--|
|ID|c36acc8a-088f-4043-ac28-4b1342409a0b|
|Source|41991954421|
|Destination|41996754421|
|StartCall|2018-01-01T10:00:00+00:00|
|EndCall|2018-01-01T00:10:30+00:00|
|StandingCharge|0.36|
|CallCharge|0.09|