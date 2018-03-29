### Downloading Geo Data

The Census/ACS is not only responsible for some of the largest data collection protocols on the planet, but it also employs hundreds of geographic data specialists and surveyors to produce highly detailed records of our natural and political boundaries. 

This branch of the Census Bureau's efforts has fallen under the Topologically Integrated Geographic Encoding and Referencing (TIGER) database initiative, which strove to standardize the United States geographic record-keeping. It just celebrated its 25th anniversary of producing high-quality geo-data for governmental, academic, and public use.

Because Census professionals prepares TIGER data, they strive to produce geographic data features that match the same geographic boundaries that delimit Census survey entities. This means that whenever we query the census, we often could download and prepare an appropriate set of geographic vectors from TIGER. 

In general, TIGER shapefiles are available in a set of three different resolutions. 1:500,000 (500k), 1:5,000,000 (5m), and 1:20,000,000 (20m) in decreasing order of precision. In general, when rendering for a web browser, we will be simplifying these, so the lower resolution files are easier to work with. But, if your map needs to be zoomed in at all, grab higher resolution data!

Visit [TIGER](https://www.census.gov/geo/maps-data/data/tiger-cart-boundary.html), where you can navigate around and access the many resouces available. TIGER downloads are zip folders full of *shapefile* data, which will need to be converted over the next few steps.

We also can [grab files directly](https://www2.census.gov/geo/tiger/GENZ2016/shp/) from a long list, which is often easier than navigating the website. That link is to the 2016 geographic data, change the URL to access different years.

-----

Also, importantly, TIGER has the absolute best logo, ever.

![rawr!](https://upload.wikimedia.org/wikipedia/commons/thumb/e/e4/US-Census-TIGERLogo.svg/440px-US-Census-TIGERLogo.svg.png)

-----

Let's explore what's [inside TIGER resources](shapefiles.md).
