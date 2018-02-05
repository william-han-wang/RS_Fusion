# Remote Sensing Fusion with Social Media Data

## Project Proposal

The data fusion has been an emerging trend in Data Science, where different modalities of data are deployed for great inference capability. Among its many meaningful applications, monitoring our planet Earth for natural hazard detection or economic activities holds great value, and demands a rich set of data modalities for better insight delivery. Features derived from a single sensor is usually very limited that one needs to consider supplementary information, leading to big data strength as well as immense challenges. 

In this project, we propose to consider data fusion in the realm of remote sensing data, where a large volume of remote sensing imagery rich in both temporal and spatial resolution is available; however, labels are usually extremely limited for remote sensing imagery in order for a large set of machine learning methods to work; this poses a big challenge in recognition-related tasks. On the other hand, data sources from social media provides rich volunteering labels with almost no cost for labeling labor. 

In the exploratory data analysis, I have considered exploiting data from tweet labels with geo-locations which indicate flood by tweet users, together with remote sensing data from sources such as [Landsat 8](https://en.wikipedia.org/wiki/Landsat_8). The goal was to develop a semi-supervised learning with noisy labels for the hazardous flood detection. A preliminary exploration showed that using only the geo-locations of the tweets (GPS enabled) with flood hashtags perform poorly due to tremendous noise in the labeling data. However, it is possible to control the error by relating the locations of flood to recorded prior knowledge of historic flood locations. This consideration funnels social media data into better label set for further critical data analysis. 

With the availability of data set provided by Planet Inc. through their open research program, one can access remote sensing database of California on a daily basis with satellite images from *Rapideye* and *Planetscope*. In this project I plan to build a data fusion program collecting both Planet satellite data and tweets with geo-locations reporting certain event, e.g., wild fires, and deliver real-time estimation of the scope of the event and affected regions. 

## Description of Data Sources

### Remote sensing data
Remote sensing data is accessible through the API of [Planet Labs](https://www.planet.com/docs/reference/data-api/). 

The [Open California dataset](https://www.planet.com/products/open-california/) consists of high-quality data collected by the RapidEye satellite, Dove satellite, together with Landsat 8 and Copernicus Sentinel-2 data (most available from 2013 onward) over California.

### Social media data
Twitter provides a developer platform to filter the tweets in real time. 
We use [Twitter API](https://developer.twitter.com/en/docs) for tweets data collections.

## Flood Detection 

Colorado flood in Sept. 2013 caused huge damage to the city Boulder. We visualize the locations of tweets during the flood event with hashtags such as #floods, #coloradoflood, etc. On the figure below, the locations of those tweets (on the left) are compared with the true flood regions released by the government after the flood event (on the right). Among all the tweets we collected, about 10% come with GPS enabled locations. There are as many as one hundred tweets or so among the geo-located tweets located near the flood region, but there are also a large portion of tweets whose locations are noisy and away from the true flooding spots. This critical issue hampers the effectiveness of using tweets locations to infer the flooded region. 
![The flooding locations with tweets](/flood/figs/tweets_flood.jpg)

We managed to relocate the noisy locations according to tweets closer to historic flood regions (on the left figure below where the hidden coordinates are longitude and latitude of flooding locations). The method is an [optimal transport scheme](http://pot.readthedocs.io/en/stable/) and later we applied the relocated tweets to a maximum entropy model for density estimation (right figure below). The result shows that this helps correct the locational bias of tweets, and improved the performance of ROC for flood density estimation. Further study is desired for a refined validation of locations for certain event(s). 

![Relocation and ROC curves under maximum entropy model](/flood/figs/results.jpg)




