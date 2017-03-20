# Evolution of the Tweet metadata, and details for effectively querying historical data
+ [Introduction](#introduction)
+ [Twitter Historical Products](#historicalProducts)
+ [Twitter JSON Objects 101](#twitterJsonIntro)
+ [Upcoming articles:](#articleList)
+ [Twitter Platform Timeline](#twitterTimeline)
+ [Historical PowerTrack: metadata and filtering timelines](#hptTimeline)
+ [Full-Archive Search API: metadata and filtering timelines](#fasTimeline)

### tl;dr
“As someone doing historical research with Twitter Data, I need to understand how the platform has evolved, how that evolution affected user behavior, how it affected the Tweet JSON payloads, and how to effectively search the Twitter archive. “

## Introduction <a id="introduction" class="tall">&nbsp;</a>

Billions of Tweets have been posted since 2006. These Tweets encapsulate an amazing amount of human communications. This archive can be an indispensable research tool for an amazing number of use-cases. 

[Set-up the reason the following details are useful]

#### New user conventions and use-patterns driving product development

Hashtags, Repies, Mentions, Retweets, adding links, sharing photos.

#### New features being added to Platform

Private messages, Ads platform, Polls.

### Twitter Historical Products <a id="historicalProducts" class="tall">&nbsp;</a>

Twitter offers two products that provide access to every publicly available Tweet; [Historical PowerTrack](http://support.gnip.com/apis/historical_api2.0/) and [Full-Archive Search](http://support.gnip.com/apis/search_full_archive_api/). These APIs able users to build queries using a set of [PowerTrack Operators](http://support.gnip.com/apis/search_full_archive_api/rules.html#Operators). 

In 2012, Historical PowerTrack (HPT) was introduced and quickly because a widely utilized Twitter research tool. HPT enables users to associate a time period of interest and a set of 1,000 PowerTrack rules/filters to an historical ```Job```. HPT offers the same Operators as real-time PowerTrack and is built to deliver Tweets at scale. In fact, this product is used to generate and share the entire public archive of Tweets to the Library of Congress (LOC). HPT generates a time-series of 10-minute data files for download. These Jobs can result in thousands of large files that take many hours to both generate and download. The HPT API provides a variety of methods to create and monitor a Job's process. Essentially the API is used to manage a Job's lifecycle. 

In 201#, the 30-Day Search API was released. [Product description. ] Next Twitter indexed the entire Tweet archive and in 2015 released Full-Archive Search (FAS). FAS also provides access to the entire Twitter archive, but does it in a much different way. With FAS you submit a single query and receive a response in classic RESTful fashion. FAS implements 500-Tweets-per-response pagination, and defaults to a 120-requests-per-minute rate-limit. Given these details, FAS can be used to rapidly retrieve Tweets, and at large scale using concurrent requests. FAS also provide the ability to count the number of Tweets matching your query before requesting the corresponding data. Counts are avaialable in arrays with minute, hour, and day periods. This ability to 'look before you leap' is an amazing tool in itself. With many use-cases, matching volumes is of primary interest. Since the Counts endpoint provides fast feedback on the matching behavior of a rule, it can be used to assess filtering behavior before pulling the data. For this reason, the Search API is a great complement to real-time and Historical PowerTrack. 


### Twitter JSON Objects 101 <a id="twitterJsonIntro" class="tall">&nbsp;</a>

Tweets are made up of a Tweet message, a posted time, a set of User (or Author or Actor) attributes, a collection of engagement metadata, and sometimes geographical metadata.

+ Tweet body
+ User object
+ Twitter entities
+ Data enrichments
+ Geo 


### Next Steps 
What follows is a set of articles that address how these Twitter changes affect the effort to find and analyze Twitter data.

[Intro narrative on the evolution of hashtags and retweets, and how new twitter features affected user-behavior.]

We'll start with a review of Twitter Plaform updates that in some way affected the JSON generated with HPT and FAS. Then we'll dig into the many product-specific details that affect how this stored JSON matches PowerTrack Operators. At the architectural level, the HPT and FAS archives are significantly different. [two slightly different list of available PowerTrack Operators.] 


# Articles <a id="articleList" class="tall">&nbsp;</a>

## Twitter timeline <a id="twitterTimeline" class="tall">&nbsp;</a>  

User-driven conventions and new features.

Looking at Twitter as a platform, the following events somehow affected the JSON payloads that are used to encode Tweets. This Tweet JSON is a set of Tweet attributes, and these metadata provide the values that PowerTrack Operators match. 

#### 2006
+ October - @replies becomes a convention. 
+ November - Favorites introduced.
#### 2007
+ January - @replies become a first-class object with a UI reply button with ```in_reply_to``` metadata. 
+ April - Retweets become a convention.
+ August #hashtags becomes a tool for searching and organizing Tweets. 
#### 2009
+ February - $cashtags become a convention for discussing stock ticker symbols. 
+ May - Twitter begins making Retweets a first-class object with ```retweet_status``` metadata. 
#### 2010
+ June - Twitter Places introduced for geo-tagging Tweets. 
#### 2016

Other important platform updates:
#### 2010
+ Tweet button launched. This made sharing links easier, so likely increased the number of URLs being shared.
#### 2011
+ Native photos introduced. 
#### 2016
+ dwm140, part 1
#### 2017
+ dmw140, part 2 





## Choosing an historical API <a id="twitterTimeline" class="tall">&nbsp;</a>  


<style type="text/css">
.tg  {border-collapse:collapse;border-spacing:0;}
.tg td{font-family:Arial, sans-serif;font-size:14px;padding:10px 5px;border-style:solid;border-width:1px;overflow:hidden;word-break:normal;}
.tg th{font-family:Arial, sans-serif;font-size:14px;font-weight:normal;padding:10px 5px;border-style:solid;border-width:1px;overflow:hidden;word-break:normal;}
.tg .tg-f3f0{font-weight:bold;background-color:#90d679;vertical-align:top}
.tg .tg-nhkk{font-weight:bold;background-color:#86baf4;vertical-align:top}
.tg .tg-yw4l{vertical-align:top}
.tg .tg-4qcj{background-color:#90d679;vertical-align:top}
.tg .tg-3we0{background-color:#ffffff;vertical-align:top}
</style>
<table class="tg">
  <tr>
    <th class="tg-nhkk">Operator</th>
    <th class="tg-nhkk">PowerTrack (real-time and Historical)</th>
    <th class="tg-nhkk">Search APIs (30-Day and Full-Archive)</th>
  </tr>
  <tr>
    <td class="tg-yw4l">"exact phrase match"</td>
    <td class="tg-4qcj">✔</td>
    <td class="tg-4qcj">✔</td>
  </tr>
  <tr>
    <td class="tg-yw4l">@</td>
    <td class="tg-4qcj">✔</td>
    <td class="tg-f3f0">✔</td>
  </tr>
  <tr>
    <td class="tg-yw4l">#</td>
    <td class="tg-4qcj">✔</td>
    <td class="tg-4qcj">✔</td>
  </tr>
  <tr>
    <td class="tg-yw4l">$</td>
    <td class="tg-4qcj">✔</td>
    <td class="tg-4qcj">✔</td>
  </tr>
  <tr>
    <td class="tg-yw4l">bio:</td>
    <td class="tg-4qcj">✔</td>
    <td class="tg-yw4l"></td>
  </tr>
  <tr>
    <td class="tg-yw4l">bio_location:</td>
    <td class="tg-4qcj">✔</td>
    <td class="tg-yw4l"></td>
  </tr>
  <tr>
    <td class="tg-yw4l">bio_name:</td>
    <td class="tg-4qcj">✔</td>
    <td class="tg-yw4l"></td>
  </tr>
  <tr>
    <td class="tg-yw4l">bounding_box:</td>
    <td class="tg-4qcj">✔</td>
    <td class="tg-4qcj">✔</td>
  </tr>
  <tr>
    <td class="tg-yw4l">contains:</td>
    <td class="tg-4qcj">✔</td>
    <td class="tg-yw4l"></td>
  </tr>
  <tr>
    <td class="tg-yw4l">&lt;emoji&gt;</td>
    <td class="tg-4qcj">✔</td>
    <td class="tg-yw4l"></td>
  </tr>
  <tr>
    <td class="tg-yw4l">followers_count:</td>
    <td class="tg-4qcj">✔</td>
    <td class="tg-yw4l"></td>
  </tr>
  <tr>
    <td class="tg-yw4l">friends_count:</td>
    <td class="tg-4qcj">✔</td>
    <td class="tg-yw4l"></td>
  </tr>
  <tr>
    <td class="tg-yw4l">from:</td>
    <td class="tg-4qcj">✔</td>
    <td class="tg-4qcj">✔</td>
  </tr>
  <tr>
    <td class="tg-yw4l">has:geo</td>
    <td class="tg-4qcj">✔</td>
    <td class="tg-4qcj">✔</td>
  </tr>
  <tr>
    <td class="tg-yw4l">has:hashtags</td>
    <td class="tg-4qcj">✔</td>
    <td class="tg-4qcj">✔</td>
  </tr>
  <tr>
    <td class="tg-yw4l">has:images</td>
    <td class="tg-4qcj">✔</td>
    <td class="tg-4qcj">✔</td>
  </tr>
  <tr>
    <td class="tg-yw4l">has:lang</td>
    <td class="tg-4qcj">✔</td>
    <td class="tg-yw4l"></td>
  </tr>
  <tr>
    <td class="tg-yw4l">has:links</td>
    <td class="tg-4qcj">✔</td>
    <td class="tg-4qcj">✔</td>
  </tr>
  <tr>
    <td class="tg-yw4l">has:media</td>
    <td class="tg-4qcj">✔</td>
    <td class="tg-4qcj">✔</td>
  </tr>
  <tr>
    <td class="tg-yw4l">has:mentions</td>
    <td class="tg-4qcj">✔</td>
    <td class="tg-4qcj">✔</td>
  </tr>
  <tr>
    <td class="tg-yw4l">has:profile_geo</td>
    <td class="tg-4qcj">✔</td>
    <td class="tg-4qcj">✔</td>
  </tr>
  <tr>
    <td class="tg-yw4l">has:symbols</td>
    <td class="tg-4qcj">✔</td>
    <td class="tg-4qcj">✔</td>
  </tr>
  <tr>
    <td class="tg-yw4l">has:videos</td>
    <td class="tg-4qcj">✔</td>
    <td class="tg-4qcj">✔</td>
  </tr>
  <tr>
    <td class="tg-yw4l">in_reply_to_status_id:</td>
    <td class="tg-4qcj">✔</td>
    <td class="tg-yw4l"></td>
  </tr>
  <tr>
    <td class="tg-yw4l">is:quote</td>
    <td class="tg-4qcj">✔</td>
    <td class="tg-yw4l"></td>
  </tr>
  <tr>
    <td class="tg-yw4l">is:retweet</td>
    <td class="tg-4qcj">✔</td>
    <td class="tg-4qcj">✔</td>
  </tr>
  <tr>
    <td class="tg-yw4l">is:verified</td>
    <td class="tg-4qcj">✔</td>
    <td class="tg-4qcj">✔</td>
  </tr>
  <tr>
    <td class="tg-yw4l">keyword</td>
    <td class="tg-4qcj">✔</td>
    <td class="tg-4qcj">✔</td>
  </tr>
  <tr>
    <td class="tg-yw4l">lang:</td>
    <td class="tg-4qcj">✔</td>
    <td class="tg-4qcj">✔</td>
  </tr>
  <tr>
    <td class="tg-yw4l">listed_count:</td>
    <td class="tg-4qcj">✔</td>
    <td class="tg-yw4l"></td>
  </tr>
  <tr>
    <td class="tg-yw4l">place_country:</td>
    <td class="tg-4qcj">✔</td>
    <td class="tg-4qcj">✔</td>
  </tr>
  <tr>
    <td class="tg-yw4l">place:</td>
    <td class="tg-4qcj">✔</td>
    <td class="tg-4qcj">✔</td>
  </tr>
  <tr>
    <td class="tg-yw4l">point_radius:</td>
    <td class="tg-4qcj">✔</td>
    <td class="tg-4qcj">✔</td>
  </tr>
  <tr>
    <td class="tg-yw4l">profile_bounding_box</td>
    <td class="tg-4qcj">✔</td>
    <td class="tg-yw4l"></td>
  </tr>
  <tr>
    <td class="tg-yw4l">profile_country:</td>
    <td class="tg-4qcj">✔</td>
    <td class="tg-4qcj">✔</td>
  </tr>
  <tr>
    <td class="tg-yw4l">profile_locality:</td>
    <td class="tg-4qcj">✔</td>
    <td class="tg-4qcj">✔</td>
  </tr>
  <tr>
    <td class="tg-yw4l">profile_point_radius</td>
    <td class="tg-4qcj">✔</td>
    <td class="tg-yw4l"></td>
  </tr>
  <tr>
    <td class="tg-yw4l">profile_region:</td>
    <td class="tg-4qcj">✔</td>
    <td class="tg-4qcj">✔</td>
  </tr>
  <tr>
    <td class="tg-yw4l">profile_subregion:</td>
    <td class="tg-4qcj">✔</td>
    <td class="tg-yw4l"></td>
  </tr>
  <tr>
    <td class="tg-yw4l">proximity~N</td>
    <td class="tg-4qcj">✔</td>
    <td class="tg-4qcj">✔</td>
  </tr>
  <tr>
    <td class="tg-yw4l">retweets_of_status_id:</td>
    <td class="tg-4qcj">✔</td>
    <td class="tg-yw4l"></td>
  </tr>
  <tr>
    <td class="tg-yw4l">retweets_of:</td>
    <td class="tg-4qcj">✔</td>
    <td class="tg-4qcj">✔</td>
  </tr>
  <tr>
    <td class="tg-yw4l">sample:</td>
    <td class="tg-4qcj">✔</td>
    <td class="tg-3we0"></td>
  </tr>
  <tr>
    <td class="tg-yw4l">source:</td>
    <td class="tg-4qcj">✔</td>
    <td class="tg-yw4l"></td>
  </tr>
  <tr>
    <td class="tg-yw4l">statuses_count:</td>
    <td class="tg-4qcj">✔</td>
    <td class="tg-yw4l"></td>
  </tr>
  <tr>
    <td class="tg-yw4l">time_zone:</td>
    <td class="tg-4qcj">✔</td>
    <td class="tg-yw4l"></td>
  </tr>
  <tr>
    <td class="tg-yw4l">to:</td>
    <td class="tg-4qcj">✔</td>
    <td class="tg-4qcj">✔</td>
  </tr>
  <tr>
    <td class="tg-yw4l">url_contains:</td>
    <td class="tg-4qcj">✔</td>
    <td class="tg-yw4l"></td>
  </tr>
  <tr>
    <td class="tg-yw4l">url_description:</td>
    <td class="tg-4qcj">✔</td>
    <td class="tg-yw4l"></td>
  </tr>
  <tr>
    <td class="tg-yw4l">url_title:</td>
    <td class="tg-4qcj">✔</td>
    <td class="tg-yw4l"></td>
  </tr>
  <tr>
    <td class="tg-yw4l">url:</td>
    <td class="tg-4qcj">✔</td>
    <td class="tg-4qcj">✔</td>
  </tr>
</table>





## Historical API: metadata and filtering timeline  <a id="hptTimeline" class="tall">&nbsp;</a>

### Product timeline

### Metadata timelines
#### 2007
+ January 3 - is:verified begins matching.
#### 2008
+ February 27 - ```has:mentions``` and ```has:links``` begins matching.
#### 2011
+ September 1 - Tweet Geo starts. Matching for *has:geo, place_country:, bounding_box: point_radius:*.
#### 2012
+ March 26 
    - Gnip Language - ```gnip.lang``` language metadata. No longer filtered for. ```lang:``` Operator now based solely on root level Twitter language classification. 
    - Expanded URLs - URL metadata from this date until launch of HPT 2.0 will contain ```gnip.expanded_url``` fully unwound URL. 
    - Klout Scores - Klout scores from this date until launch of HPT 2.0 will contain ```gnip.klout_score``` data.
#### 2013
+ March 26 - Twitter language classifiction added. 
+ June 4 - Profile Geo launched.
#### 2015
+ September 28 - is:quote begins matching. 
#### 2017
+ February 22 - Poll metadata is available in *original* format. 



## Search API and metadata timeline

## Full-Archive Search API: metadata and filtering timeline  <a id="d=fasTimeline" class="tall">&nbsp;</a>

+ User/Actor object metadata updated at query time. 
 
+ Tweet engagement metadata updated at query time.



### Product timeline


### Metadata JSON timelines

Below are details about when Operator behavior changed. 

#### 2006
 + July 13 - ```has:mentions``` begins matching.
 + October 6 - ```has:symbols``` begins matching (Search). $cashtags for discussing stock symbols does not become common until early 2009.
 + October 26 - ```has:links``` begins matching.
 + November 23 - ```has:hashtags``` begins matching.

#### 2007
 + January 30 - First first-class @reply (in_reply_to_user_id), ```reply_to_status_id:``` begins matching. 
 + August 23 - “hashtag invented” according to internal history. First real use a week later.

#### 2009
+ May 15 - ```is:retweet``` begins matching.  

#### 2010
+ March 6 - ```has:geo``` starts matching. 

### Filtering

+ geo operators
+ User/Actor metadata
+ URL matching

[] is:verified support throughout Search archive. 
[] is:quote not available - strategies for matching in Search?
