### Converting Shapefiles

Geographic data from the census arrives in an unwiedly, ancient, binary  format designed for use in GIS software. The data is split over many different files, which need to be operated on together.

Illinois, in 2016, at the 5m resolution looks like this once unzipped.

```
cb_2016_us_state_5m.cpg
cb_2016_us_state_5m.dbf
cb_2016_us_state_5m.prj
cb_2016_us_state_5m.shp
cb_2016_us_state_5m.shp.ea.iso.xml
cb_2016_us_state_5m.shp.iso.xml
cb_2016_us_state_5m.shp.xml
cb_2016_us_state_5m.shx
```

The most important files are the `.shp` file, which contains the actual geo-data, the `.prj` file, which contains information on the projection and coordinate system used (if not lon-lat), and the `.dbf` file, which contains additional data tied to each vector. 

We need to remember that these many files all interrelate, and the loss of any one of them might cause things to break unexpectedly.

-----

As mentioned above, the `.shp` file is a geographic vector file. We can peak at its contents, where we might expect a list of coordinates.

```
0000 270a 0000 0000 0000 0000 0000 0000
0000 0000 0000 0000 000a 65e4 e803 0000
0500 0000 902c 6002 b764 66c0 00e0 d8b3
e71a 2dc0 59dd ea39 e978 6640 1536 035c
90d6 5140 0000 0000 0000 0000 0000 0000
0000 0000 0000 0000 0000 0000 0000 0000
0000 0000 0000 0001 0000 18f6 0500 0000
6325 e659 491e 56c0 5c19 541b 9c38 3e40
d80e 46ec 1339 55c0 e4b9 be0f 0781 4140
0400 0000 1b03 0000 0000 0000 0700 0000
0f00 0000 2700 0000 739b 70af cc02 56c0
bd32 6fd5 7584 3e40 f166 0dde 5702 56c0
a4c3 4318 3f85 3e40 d190 f128 9501 56c0
e6af 90b9 3284 3e40 d190 f128 9501 56c0
33fa d170 ca80 3e40 44da c69f a801 56c0
...
```

Ahhh, binary! Shapefiles are highly compressed, so we can't see what they describe, nor can browsers. We need to convert these to a more usable and understandable format.

-----

Navigate in your terminal, with the `cd` command. Once there, we can use our new tools to convert the file.

```
shp2json cb_2016_us_state_5m.shp > il.json
``` 

This line converts a shapefile (and all associated datafiles) to a legible json format, and stuffs that data into a new file called `il.json`. Take a look!

```
{"type":"FeatureCollection","bbox":[-179.14733999999999,-14.552548999999999,179.77847,71.352561],"features":[{"type":"Feature","properties":{"STATEFP":"04","COUNTYFP":"015","COUNTYNS":"00025445","AFFGEOID":"0500000US04015","GEOID":"04015","NAME":"Mohave","LSAD":"06","ALAND":34475567011,"AWATER":387344307},"geometry":{"type":"Polygon","coordinates":[[[-114.755618,36.087165999999996],[-114.753638,36.090705],[-114.747079,36.097004999999996],[-114.736165,36.104366999999996],[-114.717293,36.107686],[-114.709771,36.107742],[-114.666538,36.117343],[-114.66289,36.119932],[-114.65995,36.124145],[-114.631716,36.142306],[-114.627855,36.141011999999996],[-114.621883,36.13213],[-114.616694,36.130100999999996],[-114.608264,36.133949],[-114.597212,36.142103],[-114.572031,36.15161],[-114.545789,36.152248],[-114.511721,36.150956],[-114.506711,36.148277],[-114.504631,36.145629],[-114.50482,36.142413999999995],[-114.505387,36.137496],[-114.506144,36.134659],[-114.505766,36.131444],[-114.504442,36.129740999999996],[-114.502172,36.128796],[-114.49612,36.127849999999995],[-114.487034,36.129396],[-114.470152,36.138801],[-114.463637,36.139694999999996],[-114.458369,36.138586],[-114.453325,36.130725999999996],[-114.448654,36.12641],[-114.446605,36.125969999999995],[-114.42716899999999,36.136305],[-114.41695,36.145761],[-114.412373,36.147254],[-114.405475,36.147371],[-114.372106,36.143114],[-114.363109,36.130246],[-114.337273,36.108019999999996],[-114.328777,36.105501],[-114.30843,36.082443],[-114.305738,36.074881999999995],[-114.307879,36.071290999999995],[-114.314206,36.066618999999996],[-114.316109,36.063109],[-114.315557,36.059494],[-114.314028,36.058164999999995],[-114.280202,36.046361999999995],[-114.270645,36.03572],[-114.266721,36.029238],[-114.263146,36.025937],[-114.252651,36.020193],[-114.238799,36.014561],[-114.233289,36.014289],[-114.21369,36.015613],[-114.19238,36.020993],[-114.176824,36.027651],[-114.166465,36.027
...
```

This is a long file! But, it has tons of useful data for us. The simplified structure is the following.

```js
{
	"type":"FeatureCollection",
	"bbox":[4 bounding box coordinates],
	"features":[
		{
			"type":"Feature",
			"properties":{information about each entity},
			"geometry":{
				"type":"Polygon",
				"coordinates":[array of projected lon-lat positions definining boundary]
			}
		},
		{
			"type":"Feature",
			"properties":{information about each entity},
			"geometry":{
				"type":"Polygon",
				"coordinates":[array of projected lon-lat positions definining boundary]
			}
		}
	]
}
```

A singular object is defined, which includes an array called `features`. Each `feature` in that array has a set of `properties` that will vary depending on the type of shapefile, as well as an array of `coordinates` for drawing. 

-----

Working on shapefiles with the command line is great, but sometimes we just want to move faster! You can use the wonderful [mapshaper](http://mapshaper.org) to also convert shapefiles and visualize their contents as well. Conveniently, mapshaper also can simplify shapefile boundaries to shrink filesize.

-----

But, we want more aesthetic control than shapefiles can offer. Let's [visualize geography in D3](visualize.md)!
