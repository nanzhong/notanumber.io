---
layout: post
title:  typeracer-stats
date:   2014-04-20 04:00:32 -0400
tags:   [dvorak,typeracer]
---
_Edit 2016-10-02: I haven't maintained this at all, so much of this is likely no longer correct or working_

Typing, keyboards, and ergonomics have been my latest obsession, and it has been fueled by my recent decision to switch to the Dvorak keyboard layout.

These past few weeks I've progressed as a Dvorak typist (albeit much slower than I had hoped), and besides practice from typing as part of my daily work, [typeracer.com](http://typeracer.com) has been a large part of this. 

<!--more-->

Typeracer is great practice. By breaking down the typing practice into short bursts of high concentration, I feel like it provides a good balance of allowing you to build muscle memory without getting overly strained or frustrated. However it does have its limitations. Copying text is much easier than writing text; I find that not having to think about what you have to type next allows me to almost blank out my mind, and in this state my accuracy and typing speed is higher than when I normally type. Nonetheless, typeracer's pretty great and adding in gamification definietly makes it more fun than other typing practice tools I've tried lately.

One thing that I feel that is really lacking from typeracer is meaningful statistics (or at least stats that I was able to find on the site). As a person who's actively trying to improve, I really want to know what my progress looks like. Out of the box, typeracer has support for exporting race history as a csv file (full history if you are a premium member), and it also shows your race history per race in a nice little graph, if you have typed the same race multiple times. Unfortunately, having to parse a csv file is no fun, and with the large selection of different texts for races you won't really have too much history to view per race unless you've already spent a very large amount of time on the game.

A few days ago a was a little curious, and it turns out that there is [a nice little API](https://groups.google.com/forum/#!msg/typeracer/cKCIS8cfrZE/LAGEsjMJFA4J) for querying typeracer race history. It returns JSON data, and basically there are two endpoints.


	http://data.typeracer.com/users?id=tr:<username>
    
will return basic user profile information and stats in the following form

	{
    	"premium": false,
    	"name": "Nan",
    	"hasPic": false,
    	"country": "ca",
    	"tstats": {
       		"level": "L4",
        	"recentAvgWpm": 54.1952796936,
        	"cg": 218,
        	"gamesWon": 41,
        	"wpm": 46.8831816768,
        	"certWpm": 0,
        	"recentScores": [
            	56.4904060364,
            	...
        	],
        	"bestGameWpm": 64.6342315674
    	},
    	"avatar": null,
    	"lastName": "Zhong",
    	"countryManual": false,
    	"id": "tr:nanzhong"
	}	
    
and

	http://data.typeracer.com/games?playerId=tr:<username>&amp;n=<batch_size>&amp;offset=<offset>
    
will return you race history in the form of

	[
    	{
        	"np": 3,
        	"wpm": 51.1230583191,
        	"r": 2,
        	"t": 1397950512.11,
        	"sl": "L5",
        	"tid": 278,
        	"gn": 218
    	},
        ...
	]

I may be wrong but these are the only endpoints that I was able to find. I really wish that typeracer would collect more metrics like character mistype counts, because to a typist who's trying to improve, that type of data would be extremely useful.

The one main metric that I wanted to calculate from this data is how I am progressing in terms of typing speed, so I put together a really quick and simple tool for this, [nanzhong/typeracer-stats](https://github.com/nanzhong/typeracer-stats). If anyone is interested it will show basic profile information and stats as well as the daily average typing speed. You can access it by visiting [http://typeracer-stats.nine27.com/username](http://typeracer-stats.nine27.com/username), of course replacing "username" with your own.

![nanzhong](/content/images/2014/Apr/typeracer-stats.png)

My progress has been slow but steady, and from the looks of it, I've still got a long way to go before I'm back at my Qwerty speed of ~95 WPM.
