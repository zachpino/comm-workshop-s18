### Questions, Data, and Approach

These tutorials all focus on data from the census tabulations on *commuting*, and to ensure the most voluminous data, we'll be looking at the ACS 2015, 5-year vintage.

Notably, we'll be looking at datapoints from the following ACS groups:

- B08006: SEX OF WORKERS BY MEANS OF TRANSPORTATION TO WORK
- B08011: SEX OF WORKERS BY TIME LEAVING HOME TO GO TO WORK
- B08012: SEX OF WORKERS BY TRAVEL TIME TO WORK	

Though we aren't specifically looking at gender differentials (and we'll be using estimated totals and not pulling in gender-specific data), these datapoints are the best way to prove out some potential insights on the United States' commuting behaviors.

How and why people commute is a complicated, nested set of motivations and constraints tied to all kinds of socioeconomic factors: job availability, real estate price and availability, industry locuses, school performance, taxation, infrastructure condition, presence of aligned public transporation, political identity and age, education level, topographical complexities and geopolitical boundaries... on and on. And, there may be economic or socials incentives that encourage specific commuting behaviors or discourage the capital-intensive commuting technology investments, for instance lobbying actions on behalf of various transportation types in geographic regions. Its' a tangled beast, and data viz can help us get to answers.

----

##### Hypothetical Correlation

We will begin by mapping these commuting-related datapoints in relation to one another, and as a result, our chart will start out fairly expected. This is often a good place to commence with any data visualization: plot similar, known values against one another to see if the datapoints move together as expected. This is a way to experimentally prove *correlation* or luck out and find discordant insights.

For example, we might *hypothesize* with common sense that commuters who leave early are also the ones who take a long time to get to work, since in most locales in the United States there is a set time for work to begin. If you live further away, it will take you longer to reach work on time. That is to say, *commuters leaving earlier take longer to get to work*, that **commute time is fundamentally dependent on geographic adjacency** But, of course, we should ensure that our simple hypothesis is provable in the data before moving on to research into the impact of more esoteric socioeconomic forces on commute time. This will turn out to be true.

Another *hypothesis* might interrelate public transportation and commute time. Where public transportation is available, we would expect commute times to be short — these are urban areas where travel distances are short. And indeed, we would expect urban dwellers to take public transit if and only if public transit delivered a comparable travel time relative to rush hour traffic. As we'll see, though, this seemingly reasonable *hypothesis* is totally flawed, and the inverse is true in the data.

Once these factors internal to commuting are better understood, it would be a good idea try to prove other relationships — is commuting driven by or driving other socioeconomic factors? Pun! That exercise will be left to further homework.

-----

So, we're talking about commuting. Let's move onto [building a page for visualization](container.md).
