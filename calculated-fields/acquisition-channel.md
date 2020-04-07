# Acquisition Channel

The UTM medium can sometimes lead to messy data and using a combination of regex and case statements can help clean up this field to aggregate in to higher-level channels.

When using a `CASE` statement, it is important to order cases by specific to general as the first conduition to match will be used otherwise. A general rule of thumb is that any `WHEN` that includes multiple conditions should be ordered first.

Also, note that the final value in the `ELSE` condition can be used to return the original value if it doesn't match a condition or a default value. The former can help you determine missing conditions over time.

Items addressed:
1. Properly classifying and capitalizing channels :bowtie:
2. Accounting for misspellings :no_entry:
3. Accounting for non-standard duplicates and variations :mouse: :hamster: :rabbit:
4. Using referrer when source is too generic, inaccurate or missing :warning:
5. Lacking other means, if a value for `Campaign` is present, we can infer this is a promotion and adjust the channel accordingly :crystal_ball:

The following placeholders are used to be replaced with relevant values:
`[Organization Name]`
`[Platform Name]`

```CASE
WHEN Medium = 'display' AND REGEXP_MATCH(Full Referrer, "[Platform Name]") THEN 'Account Based Advertising'
WHEN Medium = 'display' THEN 'Display'
WHEN Medium = 'ds_display' THEN 'Display
WHEN Medium = 'banner ad' THEN 'Display'
WHEN Medium = 'display%' THEN 'Display'
WHEN Medium = 'aba' THEN 'Account Based Advertising'
WHEN Medium = 'retargeting' THEN 'Retargeting'
WHEN Medium = 'programmatic' THEN 'Programmatic'
WHEN Medium = 'banner-ad' THEN 'Display'
WHEN Medium = 'banner' THEN 'Display'
WHEN Medium = 'media-buy' THEN 'Media Buy'
WHEN Medium = 'cpc' THEN 'Paid Search'
WHEN Medium = 'cpp' THEN 'Paid Search'
WHEN Medium = 'linkedin' AND Campaign != '(not set)' THEN 'Paid Social'
WHEN Medium = 'linkedin' THEN 'Organic Social'
WHEN Medium = 'twitter' AND Campaign != '(not set)' THEN 'Paid Social'
WHEN Medium = 'twitter' THEN 'Organic Social'
WHEN Medium = 'social' AND Campaign != '(not set)' THEN 'Paid Social'
WHEN Medium = 'social' THEN 'Organic Social'
WHEN Medium = 'video' AND Campaign != '(not set)' THEN 'Paid Video'
WHEN Medium = 'video' THEN 'Video'
WHEN Medium = '(none)' THEN 'Direct'
WHEN Medium = '(not set)' AND Campaign != '(not set)' THEN '[Organization Name] Promotion'
WHEN Medium = '(not set)' THEN 'Unknown'
WHEN Medium = 'organic' THEN 'Organic Search'
WHEN Medium = 'website' THEN '[Organization Name] Referral'
WHEN Medium = 'referral' THEN 'Referral'
WHEN Medium = 'email' THEN '[Organization Name] Email'
WHEN Medium = 'release' THEN 'Press Release'
WHEN Medium = '[Organization Name]' AND Campaign != '(not set)' THEN '[Organization Name] Promotion'
WHEN Medium = '[Organization Name]' THEN '[Organization Name] Referral'
WHEN Medium = '[Organization Name]-logo' THEN '[Organization Name] Referral'
WHEN Medium = 'ahlghert' THEN '[Organization Name] Referral'
WHEN Medium = 'engage email' THEN '[Organization Name] Email'
ELSE Medium END```
