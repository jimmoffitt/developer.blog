+ [Introduction](#introduction)
+ [Fundamental Differences](#differences)



## Choosing an historical API 

### Introduction <a id="introduction" class="tall">&nbsp;</a>  

Both Historical PowerTrack (HPT) and Full-Archive Search (FAS) can serve any publicly available Tweet from the entire archive, starting with the first Tweet from March 2006. To better understand ideal uses for Full-Archive Search versus those for Historical PowerTrack, it is important to have a clear understanding of the underlying technologies.

FAS is most analogous to Google, obviously another search-based tool. When you search for a particular term, Google doesn’t return or display the millions of matching results all at once. Rather, it delivers 10 results at a time per scrollable page and allows you to click “Next” for the subsequent page of 10 results… and so on, through all of the matching items returned. Like Google, the FAS tool is best-suited for delivering smaller datasets at a time with the ability to paginate for more data as needed. It is also the best solution for those situations where expediency in returns is needed. Thanks to having an index of every Tweet since the beginning of time, it offers near-immediate responses to these smaller data queries. Using FAS, the more data that matches your query the longer it will take you to retrieve all of that data through the product. This is because you will need to stitch together the paginated groups of results, one after the other, to create the complete file of all returned data. 

So FAS is designed using the classic request/response pattern, where a single PowerTrack rule is submitted and a response with matching Tweets is immediately provided. FAS can provide a maximum of 500 Tweets per response, and a ‘next’ token is provided to paginate until all Tweets  for a query are received. FAS also supports ‘count’ requests, where only the number of matching Tweets is provided, These counts are returned in a time-series of minute-by-minute, hourly, or daily totals.

Historical PowerTrack, on the other hand, can be compared to a library with copies of all the books that have been published in human existence. If you want to find every mention of a particular keyword or rule, you need to search through every page of every book to find them.  You may know the section of the library, the aisle, the shelf or even the specific book, but you still have to skim every page to find the exact matches of the search. 

HPT is built to deliver Tweets at scale using a batch, Job-based design where the API is used to move a HPT Job through multiple phases. These phases include volume estimation, Job acceptance/rejection, getting Job status, and downloading potentially many thousands of data files. Depending on the length of the request time period, Jobs can take hours or days to generate.


### Fundamental Differences <a id="differences" class="tall">&nbsp;</a>  

Here are the fundamental differences between Historical PowerTrack (HPT) and Full-Archive Search (FAS):

+ Number of rules supported per request.
    + Full-Archive Search accepts a single rule per request. Each rule can be up to 2,048 characters. 
    + A Historical PowerTrack Job can support up to 1,000 rules. 
+ API Data Response.
     + HPT generates a time-series of data files, each covering a ten-minute period. For example, each hour of data is provided in six 10-minute data files. Inside each HPT file, the JSON Tweet payloads are written in an atomic fashion, and are not presented in an JSON array. File contents need to be parsed using newline characters as a delimiter.
     + With FAS, Tweets in each response are arranged in a “results” array. A maximum of 500 Tweets are available per response and a ‘next’ token is provided if more Tweets are available. For example, if a 60-day request for a single PowerTrack rule matches 10,000 Tweets, at least 20 requests must be made of the Search API.
+ Supported PowerTrack Operators.
    + While the majority of Operators supported by HPT are also supported by FAS, there are a set of Operators not available in FAS:
       
<table class="tg">
  <tr>
    <td class="tg-yw4l">bio:</td>
    <td class="tg-yw4l">profile_bounding_box</td>
  </tr>
  <tr>
    <td class="tg-yw4l">bio_location:</td>
    <td class="tg-yw4l">profile_point_radius</td>
  </tr>
  <tr>
    <td class="tg-yw4l">bio_name:</td>
    <td class="tg-yw4l">profile_subregion:</td>
  </tr>
  <tr>
    <td class="tg-yw4l">contains:</td>
    <td class="tg-yw4l">retweets_of_status_id:</td>
  </tr>
  <tr>
    <td class="tg-yw4l">emoji</td>
    <td class="tg-yw4l">sample:</td>
  </tr>
  <tr>
    <td class="tg-yw4l">followers_count:</td>
    <td class="tg-yw4l">source:</td>
  </tr>
  <tr>
    <td class="tg-yw4l">friends_count:</td>
    <td class="tg-yw4l">statuses_count:</td>
  </tr>
  <tr>
    <td class="tg-yw4l">has:lang</td>
    <td class="tg-yw4l">time_zone:</td>
  </tr>
  <tr>
    <td class="tg-yw4l">in_reply_to_status_id:</td>
    <td class="tg-yw4l">url_contains:</td>
  </tr>
  <tr>
    <td class="tg-yw4l">is:quote</td>
    <td class="tg-yw4l">url_description:</td>
  </tr>
  <tr>
    <td class="tg-yw4l">listed_count:</td>
    <td class="tg-yw4l">url_title:</td>
  </tr>
</table>

+ See [HERE](https://github.com/jimmoffitt/developer_advocate.blog/blob/master/HistoricalOperatorsTable.md) for a side-by-side comparison of available Operators.
+ For a complete list of Operators for each product see here:
    + [Search Operator List](http://support.gnip.com/apis/search_full_archive_api/rules.html#Operators)
    + [Historical PowerTrack Operator List](http://support.gnip.com/apis/powertrack2.0/rules.html#Operators)
        

### How do I choose one over the other?
A general assumption to be made here is that Full-Archive Search is better-suited for lower-volume jobs, while Historical PowerTrack is more appropriate for higher-volume jobs and use cases. We’ve intentionally left those descriptions relatively vague, though, as there is no real technical reason why Full-Archive Search could not be used for large data requests. It is just not necessarily practical or efficient, so Historical PowerTrack is a good first choice for retrieving Tweets at scale, where a result set is in the millions of Tweets.
 
### Is there a technical decision point or threshold event?
Depending on how you plan to retrieve the data and utilize rate limits, there actually is a threshold where Historical PowerTrack actually processes the data faster that Full-Archive Search. HPT typically processes a 30-day duration job in about 4 hours, regardless of the volume of matching data returns. To pull 3.5M Tweets via Full-Archive Search, it would require a minimum of 7000 search requests. If you also assume 2 second response times and the need to serially paginate through the data, it would actually take Full-Archive Search longer to pull all of the Tweets.

Keep in mind that Full-Archive Search responses are capped at a maximum of 500 results in part because the technology and infrastructure that the Search APIs are built upon aren’t designed to instantly deliver large volumes of data. There are optimizations you can make to retrieve the data faster via Full-Archive Search through parallel requests, but we can discuss those separately.

Historical PowerTrack is also better suited for large query rulesets, as the Search API products only support a single PowerTrack rule per request. HPT, on the other hand, supports up to one thousand (1,000) rules. Historical PowerTrack is also the right product if you require certain operators that aren’t currently supported in Full-Archive Search (see above). 

### Are there other reasons to choose HPT over Search?
Historical PowerTrack is also a better solution for large, complex rules sets and/or use of certain filters.  Historical PowerTrack supports up to 1000 complex rules per job whereas Search is limited to a single rule per request.  That means to pull data for 1000 rules via search for 6 months, I'd have to send a minimum of 6000 requests to the Full-Archive Search API as opposed to a single HPT job.  Doing so becomes complex, costly and time consuming.  There are also a number of operators that are supported by Historical PowerTrack that are not currently or may never be supported by our search products. Some operators supported by PowerTrack and Historical PowerTrack are extremely expensive or difficult to support in a search product, they simply aren't well suited for the underlying Search technologies.  Operator support is also much more expensive for search than it is for PowerTrack and HPT, and in some cases customer usage levels and the associated revenue do not justify the cost of supporting them in Search.

### Switching between products

Many of our customers use both HPT and FAS. If you are new to both, or one of these, below are checklists that describe steps to migrate a historical request from one product to that other. 

#### Steps for converting a HPT Job to Full-Archive Search:

+ Integrate the Full-Archive Search (FAS) API.
    + FAS product documentation is available [HERE](http://support.gnip.com/apis/search_full_archive_api/).
    + FAS API documentation is available [HERE](http://support.gnip.com/apis/search_full_archive_api/api_reference.html).
    + If already using 30-Day Search, the same code used for 30-Day Search can be used for Full-Archive Search.
    + Example client code is available [HERE](http://support.gnip.com/code/search_api.html).
+ Review HPT rules and confirm all Operators are supported by Search API.
+ Multiple rules associated with a HPT Job need to be split up into individual Search requests. Each rule will be individually requested from the FAS API.
+ When receiving API responses:
    + Tweets are returned in a “results” array, starting with most recent Tweets.
    + A maximum of 500 Tweets are provided per response.
    + A ‘next’ token is provided if more requests are needed to complete request. The ‘next’ token should be parsed from the response and added to the next API request.

#### Steps for converting FAS requests to a HPT Job:

+ Integrate the Historical PowerTrack (HPT) API.
    + HPT product documentation is available [HERE](http://support.gnip.com/apis/historical_api2.0/).
    + HPT API documentation is available [HERE](http://support.gnip.com/apis/historical_api2.0/api_reference.html).
    + Example client code is available [HERE](http://support.gnip.com/code/historical_powertrack.html).
+ All FAS Operators are supported with HPT, so all rules should migrate over without revisions.
    + [Note any changes in matching behavior...]    
+ If you have a use-pattern where you query a common time period with multiple queries, these queries should be combined into a single HPT Job. 
+ The HPT API is used to advance a Job through its life cycle. 
    + When the Job is completed, a *Data URL* is generated taht provides an array of files to download. 
    + A data file is created for each 10-minute period with a matching Tweet. 
    + Tweets are written to these files in an atomic fashion, and are not placed in a JSON array. Tweets are delimited with new line characaters. 
    