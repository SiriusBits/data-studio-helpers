# Business Area

This field uses another calculated filed, the [Gated Offer field](https://github.com/SiriusBits/data-studio-helpers/blob/master/calculated-fields/gated-offer.md), for it's calculation. This simplifies the aggregation of business area that is already determined in the Gated Offer labels. 

```SQL
CASE
WHEN REGEXP_MATCH(Gated Offer, "^ALL - Gartner.*|^ALL - Forrester.*") THEN 'Analyst Relations'
WHEN REGEXP_MATCH(Gated Offer, "^ALL - Digital Transformation.*") THEN 'Universal Theme'
WHEN REGEXP_MATCH(Gated Offer, "^NV - .*") THEN 'Universal Multipurpose'
WHEN REGEXP_MATCH(Gated Offer, "^[Industry Abbreviation] - .*") THEN '[Industry]'
WHEN REGEXP_MATCH(Gated Offer, "^[Business Area] - .*") THEN '[Business Area]'
ELSE Gated Offer END
```
