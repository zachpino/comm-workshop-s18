### Questions, Data, and Approach

These tutorials all focus on data from the census tabulations on *commuting*, and to ensure the most voluminous data, we'll be looking at the ACS 2015, 5-year vintage.

Notably, we'll be looking at datapoints from the following ACS groups:

- B08006: SEX OF WORKERS BY MEANS OF TRANSPORTATION TO WORK
- B08011: SEX OF WORKERS BY TIME LEAVING HOME TO GO TO WORK
- B08012: SEX OF WORKERS BY TRAVEL TIME TO WORK	

Though we aren't specifically looking at gender differentials (and we'll be using estimated totals and not pulling in gender-specific data), these datapoints are the best way to prove out some potential insights on the United States' commuting behaviors.

How and why people commute is a complicated, nested set of motivations and constraints tied to all kinds of socioeconomic factors: job availability, real estate price and availability, industry locuses, school performance, taxation, infrastructure condition, presence of aligned public transporation, age, topogarphical complexities and geopolitical boundaries... on and on. 

We will map these commuting-related datapoints in relation to one another, and as a result, our chart will be fairly expected. This is often a good place to start with any data visualization: plot known values against one another to see if the datapoints move together as expected. This is a way to experimentally prove *correlation*.

For example, we might *hypothesize* with common sense that commuters who leave early are also the ones who take a long time to get to work, since in most locales in America there is a set time for work to begin. If you live further away, it will take you longer to reach work on time. But, of course, we should ensure that our hypothesis is present in the data before moving on to research into the impact of more distant socioeconomic forces on commute time. 

Another *hypothesis* might interrelate public transportation and commute time. Where public transportation is available, we would expect commute times to be short — these are urban areas where travel distances are short. And indeed, we would expect urban dwellers to take public transit if and only if public transit delivered a comparable travel time relative to rush hour traffic. As we'll see, though, this seemingly reasonable *hypothesis* is totally flawed.

Once these factors internal to commuting are better understood, it would be a good idea try to prove other relationships — is commuting driven by or driving other socioeconomic factors? Pun! That exercise will be left to further homework.

-----

So, we're talking about commuting. Let's move onto [fetching that census data directly with D3](fetch.md).