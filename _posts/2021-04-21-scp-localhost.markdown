---
layout: post
title:  "scp-localhost!"
date:   2021-04-21 12:47:14 -0500
categories: honeyPig scp-localhost
---
<p align="center">
<a href="http://192.168.0.15/scp-localhost/honeyPig">
<img src="images/logo.png" alt="Logo" width="600" height="300">
</a>
<h3 align="center">honeyPig</h3>
<p align="center">
Low interaction listener and port scan logger...visualization and web reporting (and management)
<br />
<a href="http://192.168.0.15/scp-localhost/honeyPig"><strong>Explore the docs »</strong></a>
<br />
<br />
<a href="http://192.168.0.15/scp-localhost/honeyPig">View Demo</a>
·
<a href="http://192.168.0.15/scp-localhost/honeyPig/issues">Report Bug</a>
·
<a href="http://192.168.0.15/scp-localhost/honeyPig/issues">Request Feature</a>
</p>
</p>
<!-- ToC -->
<details open="open">
<summary>Table of Contents</summary>
<ol>
<li>
<a href="#about-the-project">About honeyPig...</a>
<ul>
<li><a href="#built-with">Built With</a></li>
</ul>
</li>
<li>
<a href="#getting-started">Getting Started</a>
<ul>
<li><a href="#prerequisites">Prerequisites</a></li>
<li><a href="#installation">Installation</a></li>
</ul>
</li>
<li><a href="#usage">Usage</a></li>
<li><a href="#roadmap">Roadmap</a></li>
<li><a href="#contributing">Contributing</a></li>
<li><a href="#license">License</a></li>
<li><a href="#contact">Contact</a></li>
<li><a href="#acknowledgements">Acknowledgements</a></li>
</ol>
</details>

<!-- ABOUT THE PROJECT -->
## About The Project

[![Product Name Screen Shot][product-screenshot]](http://192.168.0.15/scp-localhost/honeyPig)

...This started as a text concatination of IP addresses from port scans with :pig: Snort rules syntax and lookup Urls for services like Shodan and Censys. Working on minimal hardware has always been a "Spec". This will run on Pi or Wifi Pineappple with minimal massaging.

Each instance of honeyPig listens to a specific port, minimally responding with socket handshake and a couple packets. Each hit is recorded to Db as a base64 string along with date/time and IP info. warPig (horneyPig) does both Geo lookup (fast) and domain and host (slow) as a separate process - both are very resource costly.

The spawner starts N instances and they then loop until they find an unmonitored port from their list to occupy.

The web app has a bunch of prebuild reporting and some admin functions. Most notably the /latest will show basic stats and most recent scan data with a refresh. 

### Built With

* [Bootstrap](https://getbootstrap.com)
* [JQuery](https://jquery.com)
* [Python](https://www.python.org/)
* [Flask](https://flask.palletsprojects.com/en/1.1.x/)
* [Rick](https://youtu.be/dQw4w9WgXcQ)


<!-- GETTING STARTED -->
## Getting Started

HoneyPig is meant to run with minimal effort and resources.
It is written mostly in Python3 and should run in ~Debian like environments without fuss.:smile:

Each instance of honeyPig can be set to listen to only one port or they can be ~spawned
to look for their own place in the list.
It will bootstrap its own db (without the web menu items) but needs a data dir in PWD (this is for your own good!)

### Caveats

* :pig: Hacking back is a bad idea. Honeypots are close. This is like walking into a rough bar with fake money hanging from your pocket...You'll get beaten up once by chance and again for being a wise-ass.
That said, the project requires that you open the ports you want to listen on to the outside whatever that may mean in your environment. (Port mapping at a router and device firewall rules minimally). Realize this is a safety feature you are disabling.

* :pig: Don't step on your own ports...It is possible to listen and host the web app on one interface. Make sure you don't have honeyPigs listening on the web app interface and port (or any other service for that matter). It may be useful to redirect port traffic to a listener pig on a less common port to avoid a needed service (ike SSH or VNC).

* :pig: Hacking back is a bad idea. There are places where honeyPig (and to a greater extent warPig/horneyPig) can do aggresive things. ~rick rolling logs etc. You should confine this to your own network or to a scope where you have permission for your payload.

* :pig: The web app is meant for simple local reporting and is not robust enough for a public facing app. If you use it like that and something bad happens, it is your own fault. 

* :pig: It is occasionally desirable to kill all the spawned pigs...this will do so by script name. 
```sh
sudo ps -ef | grep honeyPig.py | grep -v grep | awk '{print $2}' | sudo xargs kill
```

### Prerequisites

Python3 assumed?

* sqlite3
```sh
sudo apt-get install sqlite3
```
* flask-table
```sh
sudo python3 -m pip install flask-table
```
* missing module? just try this...
```sh
sudo python3 -m pip install [whatever]
```

### Installation

1. Python, Firewall allows for listen ports. 
2. Clone the repo
```sh
git clone http://192.168.0.15/scp-localhost/honeyPig.git
cd honeyPig
```

<!-- USAGE EXAMPLES -->
## Usage

### Basic (Starts with '127.0.0.1', 6666...will look for open port if 6666 is busy)
```sh
python3 honeyPig.py
```
### Params...
```sh
python3 honeyPig.py 0.0.0.0 80
```
### spawner
1. Set the "naughty places" port list.
```python
mainPig.naughty_places = [mainPig.server[1],7,8,9,3389]
```
2. Set the range size and IP (and seed port) in the spawner.
```python
for i in range(0,42):
	com = com + "python3 ./honeyPig.py '192.168.0.15' 7 & "
	```
	3. Let 'em rip. (they will loop untill each pig has found a port) :pig:
	```sh
	python3 honeyPigSpawn.py
	```
	* Keep this handy... 
	```sh
	sudo ps -ef | grep honeyPig.py | grep -v grep | awk '{print $2}' | sudo xargs kill
	```
	
	
	_For more examples, please refer to the [Documentation](https://example.com)_
	
	
	
	<!-- ROADMAP -->
	## Roadmap
	
	See :pig: the [open issues](http://192.168.0.15/scp-localhost/honeyPig/issues) for a list of proposed features (and known issues). Eventually...
	
	<!-- CONTRIBUTING -->
	## Contributing
	
	Contributions are what make the open source community such an amazing place to be learn, inspire, and create. Any contributions you make are **greatly appreciated**.
	
	1. Fork the Project
	2. Create your Feature Branch (`git checkout -b feature/AmazingFeature`)
	3. Commit your Changes (`git commit -m 'Add some AmazingFeature'`)
	4. Push to the Branch (`git push origin feature/AmazingFeature`)
	5. Open a Pull Request
	
	<!-- LICENSE -->
	## License
	Distributed under the MIT License. See `LICENSE` for more information.
	
	<!-- CONTACT -->
	## Contact
	
	scp - [@scp15487477](https://twitter.com/scp15487477) - steve.pote@protonmail.com :japanese_ogre:
	
	[![LinkedIn][linkedin-shield]][linkedin-url]
	
	Project Link: [http://192.168.0.15/scp-localhost/honeyPig](http://192.168.0.15/scp-localhost/honeyPig)
	
	
	<!-- ACKNOWLEDGEMENTS -->
	## Acknowledgements
	* [??](https://www.google.com/)
	* [Pigs](https://www.google.com/search?q=pigs)
	* [Snort](https://www.snort.org/)
	
	<!-- MARKDOWN LINKS & IMAGES -->
	<!-- https://img.shields.io/static/v1?label=<LABEL>&message=<MESSAGE>&color=<COLOR> -->
	<!-- https://www.markdownguide.org/basic-syntax/#reference-style-links -->
	[linkedin-shield]: https://img.shields.io/badge/-LinkedIn-black.svg?style=for-the-badge&logo=linkedin&colorB=555
	[linkedin-url]: https://www.linkedin.com/in/steve-pote/
	[product-screenshot]: images/screenshot.png
	
