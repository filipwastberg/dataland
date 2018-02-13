---
title: Billboard hits over time
author: Filip Wästberg
date: '2017-12-10'
slug: billboard-hits-over-time
categories:
  - Music
tags: []
---

Last year I read [this](http://kaylinwalker.com/50-years-of-pop-music/) post by Kaylin Walker who had scraped and analyzed the lyrics of all the year end billboard-hits from 1965-2015.

It was a great post on how pop music have changed over time.

I recently did a post similar to [Charlie Thompsons analysis](www.rcharlie.com/post/fitter-happier/) of Radiheads most depressing song, but instead of Radiohead I analyzed the Swedish band Kent, thus the post was in Swedish. This time however, my attention is on the international pop scene.

Briefly, Charlies original idea was to combine data from Spotify with sentiment analysis to determine which of Radioheads songs is most depressing. Charlie is also creator of the package `spotifyr`, a quick and easy wrapper for pulling track audio features from Spotify's Web API.

Spotify have a number of variables with interesting data about songs available on their service, such as valence (a song’s positivity), liveness, danceability, loudness, key, tempo, energy and so on. 

The goal here is to do an analysis similar to Kaylin's, but with data from Spotify.

First, as always, I will need the data.

# Get Spotify data
Spotify does not keep track on all the year end billboard hits for us. Neither do they provide us with the year the song was released. Therefore I will use Kaylin's original data set with the rankings (from Wikipedia) and lyrics. I will then use the data and search for all the songs against Spotifys API and retrieve data for the songs available on Spotify (notice that almost, but no all, the music in the world is on Spotify). 

Download Kaylin's data


```r
library(tidyverse)
library(knitr)
data <- url(
  "https://github.com/walkerkq/musiclyrics/blob/master/billboard_lyrics_1964-2015.csv?raw=true") %>%
  read_csv()

data %>% select(1:4) %>% head()
```

```
## # A tibble: 6 x 4
##    Rank                                     Song
##   <int>                                    <chr>
## 1     1                              wooly bully
## 2     2 i cant help myself sugar pie honey bunch
## 3     3               i cant get no satisfaction
## 4     4                      you were on my mind
## 5     5             youve lost that lovin feelin
## 6     6                                 downtown
## # ... with 2 more variables: Artist <chr>, Year <int>
```
