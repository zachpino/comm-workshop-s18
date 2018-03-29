### Preparatory Software Installations

In order to work with data prepared for professional and incredibly expensive Geographic Information System ([Arc]GIS) software, we need to install some open-source software.

-----

1. [Install Node.js](https://nodejs.org/en/), the server-side Javascript runtime environment. We need this to run D3 and other js on our computers native OS, rather than in a browser. Download and install the 'LTS' release.

Node, and its command line installer NPM, are increasingly becoming the default server technology for contemporary website and web applications, as well as native apps!

-----

2. [Install Homebrew], a package manager and software dependency manager for macOS. Paste this into Terminal if you have a Mac. Windows users can skip this step.

```
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

-----

3. Restart Computer!

-----

4. Test if Node works. In a terminal or command prompt, type this...

```
node -v
```

You should see a set of numbers like `v8.9.4`, this is the version of node installed.

Then, type this, and hope for similar results!

```
npm -v
```

-----

4. [Install GDAL](http://www.gdal.org), the Geographic Data Abstraction Library, which allows our computers to retopologize and edit lon-lat coordinates.

On macOS:

```
brew install gdal
```

On Windows, [download the most recent binary](http://www.gisinternals.com/release.php) for your system architecture and install it with default settings.

-----

5. Install D3 to your computers. This will let us run D3 code in our terminals. Though not mandatory for map drawing in browsers, often we will want to preview and edit geographic visualizations in our terminals where D3 code can run *much faster* on large datasets.

```
sudo npm install -g d3v4
```

-----

6. Install the D3 module for geographic, trigonometric data projection. Unlike when we import D3 in a browser `<script>` link, D3 for the command line is modularized into specific chunks. 

```
sudo npm install -g d3-geo-projection
```

-----

7. Install the D3 shapefile editing tools so we can convert binary GIS data to readable JSON.

```
sudo npm install -g shapefile
```

-----

8. Install a simple http server for pretending our personal computers are external web hosts.

```
sudo npm install -g http-server 
```

-----
9. Finally, let's install a library for creating and manipulating *newline-delimited*, rather than the standard *comma-delimited*, json files.

```
sudo npm install -g ndjson-cli
```

-----

Lots of new software to play with! Let's [grab some geographic data](geodata.md) to manipulate.