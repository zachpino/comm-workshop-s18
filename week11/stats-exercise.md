### Statistical Exercise

Let's explore some data using statistical methods.

-----

```html
<html>
<head>
    <title>
        Language Map 
    </title>

</head>

<body>
    
    <script src="https://d3js.org/d3.v4.min.js"></script>
    <script src="https://d3js.org/d3-scale-chromatic.v1.min.js"></script>
    <script src="https://d3js.org/d3-geo-projection.v2.min.js"></script>

    <script>

        //display variables
        var width = 1200;
        var height = 800;
        var margin = 30;

        //make an svg container for map
        var svg = d3.select('body')
            .append('svg')
            .attr('height',height)
            .attr('width',width)
        ;

        //rectangular background for map svg
        var background = svg
            .append('rect')
            .attr('x',0)
            .attr('y',0)
            .attr('width',width)
            .attr('height',height)
            .attr('fill','#ccc')
        ;

        //decide how to project spherical coordinates to cartesian coordinates
        var proj = d3.geoAlbersUsa()
            .scale(1300)
            .translate([width/2, height/2]);
        ;

        //set up path projector. this converts the coordinates to svg path drawing instructions
        var path = d3.geoPath()
            .projection(proj);

        var g = svg.append('g');

        //ask census for population statistics
        d3.text('https://api.census.gov/data/2016/acs/acs5?get=NAME,B06011_001E,B16001_002E,B01001_001E,B16001_003E,B16001_006E,B16001_009E,B16001_012E,B16001_015E,B16001_018E,B16001_021E,B16001_024E,B16001_027E,B16001_030E,B16001_033E,B16001_036E,B16001_039E,B16001_042E,B16001_045E,B16001_048E,B16001_051E,B16001_054E,B16001_057E,B16001_060E,B16001_063E,B16001_066E,B16001_069E,B16001_072E,B16001_075E,B16001_078E,B16001_081E,B16001_084E,B16001_087E,B16001_090E,B16001_093E,B16001_096E,B16001_099E,B16001_102E,B16001_105E,B16001_108E,B16001_111E,B16001_114E,B16001_117E,B16001_120E,B16001_123E,B16001_126E&for=congressional%20district:*',function(census){

            //remove brackets from census response
            var noBrackets = census.replace(/[\[\]]+/g,'')

            //convert census into usable js object, with relevant data precomputed
            var censusDataset = d3.csvParse(noBrackets, function(d){
                return {
                    name: d.NAME,
                    district: d["congressional district"],
                    fips: d.state,
                    income: +d.B06011_001E,
                    total: +d.B01001_001E,
                    onlyEnglish: +d.B16001_002E,
                    spanish: +d.B16001_003E,
                    french: +d.B16001_006E,
                    haitian: +d.B16001_009E,
                    italian: +d.B16001_012E,
                    portuguese: +d.B16001_015E,
                    german: +d.B16001_018E,
                    yiddish: +d.B16001_021E,
                    greek: +d.B16001_024E,
                    russian: +d.B16001_027E,
                    polish: +d.B16001_030E,
                    serbocroat: +d.B16001_033E,
                    ukrainian: +d.B16001_036E,
                    armenian: +d.B16001_039E,
                    persian: +d.B16001_042E,
                    gujarati: +d.B16001_045E,
                    hindi: +d.B16001_048E,
                    urdu: +d.B16001_051E,
                    punjabi: +d.B16001_054E,
                    bengali: +d.B16001_057E,
                    nepali: +d.B16001_060E,
                    minorindoeuropean: +d.B16001_063E,
                    telugu: +d.B16001_066E,
                    tamil: +d.B16001_069E,
                    dravidian: +d.B16001_072E,
                    chinese: +d.B16001_075E,
                    japanese: +d.B16001_078E,
                    korean: +d.B16001_081E,
                    hmong: +d.B16001_084E,
                    vietnamese: +d.B16001_087E,
                    khmer: +d.B16001_090E,
                    taikadai: +d.B16001_093E,
                    otherasian: +d.B16001_096E,
                    tagalog: +d.B16001_099E,
                    austronesian: +d.B16001_102E,
                    arabic: +d.B16001_105E,
                    hebrew: +d.B16001_108E,
                    amharic: +d.B16001_111E,
                    yoruba: +d.B16001_114E,
                    swahili: +d.B16001_117E,
                    navajo: +d.B16001_120E,
                    othernativeamerican: +d.B16001_123E,
                    otherminor: +d.B16001_126E,
                    romance: +d.B16001_003E + +d.B16001_006E + +d.B16001_009E + +d.B16001_012E + +d.B16001_015E,
                    germanic: +d.B16001_018E + +d.B16001_021E,
                    slavic: +d.B16001_027E + +d.B16001_030E + +d.B16001_033E + +d.B16001_036E,
                    semitic: +d.B16001_105E + +d.B16001_108E,
                    macroaltaic: +d.B16001_081E + +d.B16001_078E
                };
            })

            console.log(censusDataset);
        })


function getPearsonCorrelation(x, y) {
    var shortestArrayLength = 0;
     
    if(x.length == y.length) {
        shortestArrayLength = x.length;
    } else if(x.length > y.length) {
        shortestArrayLength = y.length;
        console.error('x has more items in it, the last ' + (x.length - shortestArrayLength) + ' item(s) will be ignored');
    } else {
        shortestArrayLength = x.length;
        console.error('y has more items in it, the last ' + (y.length - shortestArrayLength) + ' item(s) will be ignored');
    }
  
    var xy = [];
    var x2 = [];
    var y2 = [];
  
    for(var i=0; i<shortestArrayLength; i++) {
        if(typeof(x[i]) == "number" && typeof(y[i]) == "number") {
            xy.push(x[i] * y[i]);
            x2.push(x[i] * x[i]);
            y2.push(y[i] * y[i]);
        }
    }
  
    var sum_x = 0;
    var sum_y = 0;
    var sum_xy = 0;
    var sum_x2 = 0;
    var sum_y2 = 0;
  
    for(var i=0; i< shortestArrayLength; i++) {
        sum_x += x[i];
        sum_y += y[i];
        sum_xy += xy[i];
        sum_x2 += x2[i];
        sum_y2 += y2[i];
    }
  
    var step1 = (shortestArrayLength * sum_xy) - (sum_x * sum_y);
    var step2 = (shortestArrayLength * sum_x2) - (sum_x * sum_x);
    var step3 = (shortestArrayLength * sum_y2) - (sum_y * sum_y);
    var step4 = Math.sqrt(step2 * step3);
    var answer = step1 / step4;
  
    return answer;
 }
 
    </script>
</body>
</html>

```
