# Notebooks
Jupyter notebooks, R notebooks, Pluto.jl etc.

## Eva Summary: Where is suggested rate winning? Is it different in fRateSmasher than fRateCaster?

In order to run this analysis, I used the "daisy" query from Andrew Day, joining microfocals bid, lane, and award data with a customer submit data on or after 6/15/2022 and filtering to only include single-shot bids. I excluded any lane with flatbed as the mode, Canada as the origin or destination super region, or is_drop_trailer was marked as true, since these lanes are typically priced differently. 

This data set covers 174960 lanes with 564 unique bid_id. Every lane has a non-zero starting_rate_guidance submitted_RPM entry.
- Over all these lanes:
    - We were awarded 10.91% of them
    - The submitted rate was the awarded rate 9.68% of the time
    - The starting rate guidance was the awarded rate 5.1%  of the time

- Of the lanes we were awarded (that 10.91%):
  - The starting rate guidance was the award 46.78% of the time

- Partitioning on run date:
    - 94903 lanes over 304 unique bid id were run before 7-20 (fRateCaster)
        - Across all these lanes, there was a 11.2% win rate
        - Across all these lanes, the rate submitted was the awarded rate 9.39% of the time
        - Across all these lanes, the starting rate guidance was the awarded rate 6.53% of the time
        - Of the 11.2% of lanes we were awarded, the starting rate guidance was the award 58.32% of the time

    - 80057 lanes over 260 unique bid id were run on or after 7-20 (fRateSmasher)
        - Across all these lanes, there was a 10.58% win rate
        - Across all these lanes, the rate submitted was the awarded rate 10.04% of the time
        - Across all these lanes, the starting rate guidance was the awarded rate 3.42% of the time
        - Of the 10.58% of lanes we were awarded, the starting rate guidance was the award 32.3% of the time

- fRateSmasher is doing better in Reefer

### To further explore this behavior, I looked for trends by:

### Mode: 
Main Takeaways:
- fRateSmasher is more consistent in both win rates and awarding the starting rate guidance than fRateCaster
- fRateSmasher awards the starting rate guidance in Reefer lanes more than Van lanes. This is opposite of fRateCaster

By the numbers:
- Overall, we were awarded 5.8% of Reefer lanes and 11.2% of Van lanes. 
    - In fRateCaster:
        - Awarded 3.5% of Reefer and 11.65% of Van
    - In fRateSmasher:
        - Awarded 8.28% of Reefer and 10.73% of Van
- Over all lanes we were awarded, the starting rate guidance became the awarded rate in 47.1% of Van lanes and 37.7% of Reefer lanes
    - In fRateCaster awarded lanes:
        - Suggested was the award in 22% of Reefer lanes and 59% of Van lanes
    - In fRateSmasher awarded lanes:
        - Suggested was the award in 45% of Reefer lanes and 32% of Van lanes

### Origin Super Region:
Main Takeaways:
- fRateSmasher has award rates similar to fRateCaster in the South West and Pacific regions
- fRateSmasher has a higher award rate than fRateCaster in the North East Region
- The largest disparity in the percentage of awarded lanes that use the starting rate guidance between models is in the North Central, Pacific, and Midwest Regions.
- The starting rate guidance was used at a higher rate under fRateCaster across all regions

By the numbers:

Overall, our award rates by origin super region were:

| Origin Super Region | Overall | fRateCaster | fRateSmasher |
| --------------------|---------|-------------|--------------|
|North Central|6.46%|7.34%|5.59%|
|Pacific|6.49%|6.51%|6.46%|
|South East|9.58%|10.7%|8.07%|
|Midwest|12.65%|13.3%|11.9%|
|South West|13.37%|13.5%|13.2%|
|North East|13.88%|12.6%|15%|\

Of the awarded lanes, the starting rate guidance became the awarded rates:

| Origin Super Region | Overall | fRateCaster | fRateSmasher |
| --------------------|---------|-------------|--------------|
|North Central|55.94%|84.7%|18.4%|
|Pacific|40.33%|56.9%|17.6%|
|South East|44.58%|54.1%|27.1%|
|Midwest|53.75%|69.7%|32.9%|
|South West|43.44%|45.5%|41.1%|
|North East|41.1%|46.4%|36.9%|

### Destination Super Region:
Main Takeaways:
- Award rate was fairly consistent across regions
- fRateSmasher has a higher award rate than fRateCaster in the midwest 
- The largest disparity between award rates is in the North Central Region (fRateCaster higher)
- The percentage of lanes where the starting rate guidance becomes the award is fairly consistent, except the North East is slightly lower, and North Central region is higher.
- The percentage of lanes where the starting rate guidance becomes the award is below the average for all regions of fRateSmasher 

By the numbers:

Overall, our award rates by destination super region were:

| Destination Super Region | Overall | fRateCaster | fRateSmasher |
| --------------------|---------|-------------|--------------|
|Pacific|9.07%|9.12%|9.01%|
|South West|10.71%|11.7%|9.68%|
|South East|10.72%|11.1%|10.2%|
|North Central|11.2%|13.2%|8.91%|
|Midwest|11.5%|10.8%|12.4%|
|North East|11.89%|12.3%|11.5%|

Of the awarded lanes, the starting rate guidance became the awarded rates:

| Destination Super Region | Overall | fRateCaster | fRateSmasher |
| --------------------|---------|-------------|--------------|
|Pacific|45.66%|64.8%|25.5%|
|South West|44.1%|55.1%|29.9%|
|South East|48.3%|58%|34.2%|
|North Central|57.87%|76.2%|26.1|
|Midwest|48.09%|60.7%|34.7%|
|North East|40.58%|45.5%|34.6%|
