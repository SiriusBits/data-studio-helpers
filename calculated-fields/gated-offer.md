# Gated Offer

Using event tracking, one method of capturing page data is to use the current URL in the Event Label. This way, when an event is fired, its location can be determined and used for reporting. 

This can then be used to provide friendly values for a gated offer as determeioned by the URL path of the event label. This uses some regualr expression matching. NOTE: **Always** ensure matching goes from specific to general to group niche and specific items higher up. General matching can aggregate left-over items with fewer events. 

```SQL
CASE
WHEN REGEXP_MATCH(Event Label, ".*gartner.*") THEN 'ALL - Gartner Magic Quadrant'
WHEN REGEXP_MATCH(Event Label, ".*[Re-usable Gated Offer].*") THEN 'NV - [Gated Offer Label]'1
WHEN REGEXP_MATCH(Event Label, ".*/contact-us.*|.*/contato.*|.*/contactez-nous.*|.*/kontakt.*|.*/contactenos/.*") THEN 'NV - Contact Us'
WHEN REGEXP_MATCH(Event Label, ".*[Site Section]/[Content Category/Type].*") THEN '[Business Unit] - [Content Category/Type Label]'
WHEN REGEXP_MATCH(Event Label, ".*insurance/[gated offer URL].*") THEN 'IN - [Gated Offer]'
WHEN REGEXP_MATCH(Event Label, ".*insurance.*") THEN 'IN - Insurance Offers'
WHEN REGEXP_MATCH(Event Label, ".*/[topic]-whitepaper.*|.*/[topic]-case-study/.*") THEN '[Business Unit] - [Gated Offer]'
WHEN REGEXP_MATCH(Event Label, ".*accounts-payable.*") THEN 'NV - Accounts Payable Offers'
WHEN REGEXP_MATCH(Event Label, ".*/platform/.*|.*/products/.*") THEN 'NV - Product and Platform Offers'
WHEN REGEXP_MATCH(Event Label, ".*intelligent-automation.*") THEN 'NV - Intelligent Automation'
WHEN REGEXP_MATCH(Event Label, ".*digital-transformation.*) THEN 'ALL - Digital Transformation'
WHEN REGEXP_MATCH(Event Label, ".*artificial-intelligence.*") THEN 'NV - Artificial Intelligence Offers'
WHEN REGEXP_MATCH(Event Label, ".*/[Product Name]/.*|.*-[Product Name]-.*") THEN 'NV - [Product Name] Offers'
WHEN REGEXP_MATCH(Event Label, ".*/learn/.*") THEN 'NV - Learn Offers'
ELSE Event Label END 
```
