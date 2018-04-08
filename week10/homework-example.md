### Homework Example for 4/12

This particular visualizations strives to demonstrate where additional appropriations by Congress for the Bureau of Indian Affaris could be best allocated for revitalizing indigenous Native American languages. 

The Census Bureau tracks Americans self-identifying as *racially* Native American and native Alaskan — as either their single race, or as one of two races — in the ACS groups [B02001](https://api.census.gov/data/2016/acs/acs5/groups/B02001.html) and [B02010](https://api.census.gov/data/2016/acs/acs5/groups/B02010.html). Native Hawaiian counts are similarly tracked in those same ACS groups, though are aggregated separately with other Pacific Islander racial identities.

Additionally, speakers of the many [diverse and endangered native american languages](https://en.wikipedia.org/wiki/Indigenous_languages_of_the_Americas) are counted in ACS group [B16001](https://api.census.gov/data/2016/acs/acs5/groups/B16001.html), wherein counts for many different languages are exposed. Notably, Navajo is counted separately from all other Native American languages, as are the native Hawaiian languages.

By subtracting the current speakers of all Native Languages from the total Native population, we arrive at a count for the people for whom learning a native language might be of interest, and where there might be an opportunity to reinforce native identity and community bonds through lingual education. The Bureau of Indian Affairs, which allocates its budget through congressional appropriations, runs the Bureau of Indian Education — which has [ongoing mandates for foundational native language education for native youths and continuing lingual education for native adults](https://www.bia.gov/sites/bia.gov/files/assets/public/raca/national_policy_memoranda/pdf/idc1-031884_0.pdf). This visualizations identifies in several (somewhat unexpected) congressional districts where that money might be best spent to maximize the potential educational audience and hopefully aid in the preservation of linguisitic diversity on the North American continent. OK-1, OK-2, OK-3, OK-5, NM-3, AZ-1 are expected opportunities in the southwest where native populations are high, and the same is true of both AK-0 and HI-2 outside of the contiguous states. MT-0 and SD-0 are unexpectedly viable in the northern plains for language reclamation, as is NC-9 on the eastern seaboard.

This visualization also includes code for constructing a simple legend to tie the chromatic scale to real count values, making the visualization easier to read — and the opportunities more actionable.

![native language map](native.gif)

-----

Download [all of this code and necessary dependencies zipped up](nativelanguageopportunities.zip).

-----

```html
<html>
<head>
	<title>
		Native Language Opportunities Map 
	</title>

	<style>
		/* Side Pane Styles */
		#details {
			font-family: courier;
			color: #333;
			float: left;
			width: 20%;
			height: 800;
			font-size:12px;
			background-color:#ddd;
			border-top:3px solid #43246C;
			border-left:3px solid #43246C;
			border-bottom:3px solid #43246C;
			padding:5px;
			box-sizing: border-box;			
			color: #43246C;
		}

		#details a {color:#B24575;}
		
		svg{
			box-sizing: border-box;
			border:3px solid #43246C;
		}

		ul {
			list-style: none;
			margin-left: 0;
			padding-left: 0;
		}

		li:before {
			content: ">";
			padding-right: 5px;
		}

		span#district {
			font-size:14px;
		}
		

		/* Interactive Tooltip Styles */
		text#label{
			font-family:courier;
			font-size:10px;
		}


		/* Visualization Title Region Styles */
		text#title{
			font-family:courier;
			font-size:18px; 
			fill: #43246C;
		}

		text#subtitle{font-family:courier;font-size:14px; fill: #43246C;}


		/* Legend Region Styles */
		text.ticks{
			font-family:courier;
			font-size:10px; 
			fill: #43246C;
		}

		text#legendTitle{
			font-family:courier;
			font-size:12px; 
			fill: #43246C;
		}
	</style>

</head>

<body>
	<!-- Side Pane Defaults -->	
	<div id="details">
		<span id="district">District:</span>
		<ul>
			<li>Native Language Speakers:</li>
			<li>Native People:</li>
			<li>Native % of Population:</li>
			<li>Natives Speaking Native Language %: </li>
		</ul>

		<a href='https://www.bia.gov/sites/bia.gov/files/assets/public/raca/national_policy_memoranda/pdf/idc1-031884_0.pdf'>Read more</a> about the relevant Bureau of Indian Affairs policies and budgetary allocation methods for native language learning.
	</div>

	<!-- Import D3 Stuff -->
	<script src="https://d3js.org/d3.v4.min.js"></script>
	<script src="https://d3js.org/d3-scale-chromatic.v1.min.js"></script>
	<script src="https://d3js.org/d3-geo-projection.v2.min.js"></script>


	<script>
		//display variables
		var width = 1200;
		var height = 800;

		//append svg container
		var svg = d3.select('body')
			.append('svg')
			.attr('height',height)
			.attr('width',width)
			.call(d3.zoom()
				.scaleExtent([1, 5])
				.translateExtent([[-width/2, -height/2 ], [width*1.5,height*1.5]])
				.on("zoom", function () {
					g.attr("transform", d3.event.transform)
				})
			);
		;

		//rectangular background for svg container
		var background = svg
			.append('rect')
			.attr('x',0)
			.attr('y',0)
			.attr('width',width)
			.attr('height',height)
			.attr('fill','#ddd')
		;

    	//decide how to project spherical coordinates to cartesian coordinates
		var proj = d3.geoAlbersUsa()
  			.scale(1300)
  			.translate([width/2, height/2]);
  		;

		//set up path projector. this converts the coordinates to svg path drawing instructions
    	var path = d3.geoPath()
    		.projection(proj);

    	//svg group for zooming
    	var g = svg.append('g');

		//ask census for population statistics
	    d3.text('https://api.census.gov/data/2016/acs/acs5?get=NAME,B01001_001E,B02001_004E,B02001_006E,B02010_001E,B02012_001E,B16001_102E,B16001_120E,B16001_123E&for=congressional%20district:*',function(census){

	    	//remove brackets from census response
	    	var noBrackets = census.replace(/[\[\]]+/g,'')

	    	//convert census into usable js object, with relevant data precomputed
	    	var censusDataset = d3.csvParse(noBrackets, function(d){
				return {
					//geographic information		
					name: d.NAME,
					district: d["congressional district"],
					fips: d.state,
					total: +d.B01001_001E,
					//identity counts		
					soleIndigenous: +d.B02001_004E,
					soleHawaiian: +d.B02001_006E,
					dualIndiginous: +d.B02010_001E,
					dualHawaiian: +d.B02012_001E,
					//single languages counts
					hawaiian: +d.B16001_102E,
					navajo: +d.B16001_120E,
					otherIndigenous: +d.B16001_123E,
					//combination counts 
					indigenousLanguageSpeakers: +d.B16001_120E + +d.B16001_123E + +d.B16001_102E,
					indigenousPeople: +d.B02001_004E + +d.B02001_006E+ +d.B02010_001E + +d.B02012_001E,
					//opportunity counts
					indigenousOpportunityCount: (+d.B02001_004E + +d.B02001_006E+ +d.B02010_001E + +d.B02012_001E) - (+d.B16001_120E + +d.B16001_123E + +d.B16001_102E)
		      	};
	    	})

	    	//console.log(censusDataset);

	    	//map for matching data to geography
	    	var censusMap = d3.map(censusDataset, function(d){ return d.fips + d.district });

	    	//speaker data 	
	    	var indigenousLanguageMax = d3.max(censusDataset, function(d){ return d.indigenousLanguageSpeakers});
	    	var indigenousLanguageScale = d3.scalePow().exponent(.5).domain([0, indigenousLanguageMax]).range([0,1]);

	    	//identity data
	    	var indigenousPeopleMax  = d3.max(censusDataset, function(d){ return d.indigenousPeople});
	    	var indigenousPeopleScale = d3.scalePow().exponent(.5).domain([0, indigenousPeopleMax]).range([0,1]);

	    	//opportunity data
	    	var indigenousOpportunityMax  = d3.max(censusDataset, function(d){ return d.indigenousOpportunityCount});
	    	var indigenousOpportunityScale = d3.scalePow().exponent(.5).domain([0, indigenousOpportunityMax]).range([0,1]);


	    	//access geojson file, err is if we get any errors in reading the file, geojson is the geo data
	   		d3.json('congressional_districts_5m.json', function(err, geojson) {
	   		
				//draw all of the regions included in the 'features' child array
				var districts = g
					.selectAll('.districts')
					.data(geojson.features)
					.enter()
					.append("path")
					.attr("d", path)
					.attr("class","districts")
					.attr('stroke-width',0)
					.attr('stroke-opacity',.5)
					.attr('stroke','white')
					.attr('fill', function(d){
						//find matching data in census
						var match = censusMap.get(d.properties.GEOID);

						if(match){
							return d3.interpolateMagma(indigenousOpportunityScale( match.indigenousOpportunityCount ));
						}
						else{
							//no match between census and geo data
							return 'black';
						}

					})
					.on('click',function(d){
						//reset all districts and remove tooltip
						d3.selectAll('.districts').transition().duration(500).attr('stroke-width',0);
						d3.selectAll('#label').transition().duration(500).attr('opacity',0).remove();

						//add stroke to the selected district boundary
						d3.select(this).transition().duration(750).attr('stroke-width',1)

					
						//find matching data in census
						var match = censusMap.get(d.properties.GEOID);

						//catch errors if there was no match
						if(match){
							//get text data for displaying the name of the state and district number
							var name = match.name;

							//name from census looks like "Congressional District 1 (115th Congress), Arizona"
							//so, we split the string into items in an array at the comma, and get everything after the comma by getting item 1
							var state = match.name.split(',')[1]

							//we can get the district number in the same way, but by splitting at spaces and getting the second item
							var districtNumber = match.name.split(' ')[2]

							//we need to handle 'at-large' congressional districts edge cases separately
							if (districtNumber == "(at"){districtNumber = "At Large"}

							//inject new content into details side pane
							d3.select('#details').html(
								"<span id='district'>District: " + state + " " + districtNumber + "</span>" +
								"<ul>" + 
									"<li>Native Language Speakers: " + match.indigenousLanguageSpeakers.toLocaleString() + "</li>" +
									"<li>Native People: " + match.indigenousPeople.toLocaleString() + "</li>" +
									"<li>Native % of Population: " + ((match.indigenousPeople / match.total)*100).toFixed(2) + "%</li>" +
									"<li>Natives Speaking Native Language %: " + ((match.indigenousLanguageSpeakers / match.indigenousPeople)*100).toFixed(2) + "%</li>" +
								"</ul>" + 
								"<a href='https://www.bia.gov/sites/bia.gov/files/assets/public/raca/national_policy_memoranda/pdf/idc1-031884_0.pdf'>Read more</a> about the relevant Bureau of Indian Affairs policies and budgetary allocation methods for native language learning." 
								)

							//display tooltip with calculated name centered on district geography
							var label = g
								.append('text')
								.attr('id','label')
								.attr('x', path.centroid(d)[0] )
								.attr('y', path.centroid(d)[1] )
								.attr('fill', 'white')
								.attr('text-anchor','middle')
								.attr('opacity', 0)
								.text(state + " " + districtNumber)
								.transition()
								.duration(750)
								.attr('opacity', 1)
							;
						}
					})		
				;
			})

	   		//create title region at top of container
	   		var titleHeight = 70;
	   		var titlePadding = 10;

	   		//group to hold title content
	   		var titleGroup = svg.append('g');

			//background for title content
	   		var titleBackground = titleGroup
				.append('rect')
				.attr('y', -3)
				.attr('x', -3)
				.attr('height', titleHeight)
				.attr('width', width)
				.attr('fill','#ddd')
				.attr('stroke','#43246C')
				.attr('stroke-width', 3)

			//append title
			var title = titleGroup
				.append('text')
				.attr('id','title')
				.attr('x', titlePadding)
				.attr('y', titleHeight * .4)
				.text("The Future Speakers of Native Languages")
			
			//append subtitle
			var subTitle = titleGroup
				.append('text')
				.attr('id','subtitle')
				.attr('x', titlePadding)
				.attr('y', titleHeight * .7)
				.text("Which congressional districts would benefit most from increased BIA appropriations for native language recovery programs?")			

			//create legend at bottom of container
	   		var legendTicks = [0,.25,.5,.75,1];
	   		var legendHeight = 80;
	   		var legendWidth = 400;
	   		var legendPadding = 10;
	   		var legendBlockWidth = (legendWidth - (2*legendPadding)) / (legendTicks.length); 
	   		var legendBlockHeight = 20;

	   		//add svg group for legend content
	   		var legendGroup = svg.append('g')

	   		//background for legend region
	   		var legendBackground = legendGroup
				.append('rect')
				.attr('y', height - legendHeight)
				.attr('x', 0)
				.attr('height', legendHeight)
				.attr('width', legendWidth)
				.attr('fill','#ddd')
				.attr('stroke','#43246C')
				.attr('stroke-width', 3)

			//title for legend
			var legendTitle = legendGroup
				.append('text')
				.attr('id','legendTitle')
				.attr('y', height - (legendHeight * .75))
				.attr('x', legendPadding)
				.text("Native Individuals *Not* Speaking Native Languages")
			
			//legend color squares
			var legendBlocks = legendGroup
				.selectAll('.blocks')
				.data(legendTicks)
				.enter()
				.append('rect')
				.attr('class','blocks')
				.attr('x', function(d,i){ return (i * legendBlockWidth) + legendPadding})
				.attr('y', height - (legendHeight * .5) - legendBlockHeight/2)
				.attr('width', legendBlockWidth)
				.attr('height', legendBlockHeight)
				.attr('fill', function(d){return d3.interpolateMagma(d)})
			;

			//legend text ticks
			var legendLabels = legendGroup
				.selectAll('.ticks')
				.data(legendTicks)
				.enter()
				.append('text')
				.attr('class','ticks')
				.attr('x', function(d,i){ return (i * legendBlockWidth) + legendPadding})
				.attr('y', height - (legendHeight * .2))
				.text(function(d){return parseInt(d * indigenousOpportunityMax).toLocaleString() })
			;
	    })
	</script>
</body>
```
