<h2>Native Format Data Dictionary<a class="headerlink" href="#field-guide" title="Permalink to this headline">¶</a></h2>
<p>Consumers of Tweets should tolerate the addition of new fields and variance in ordering of fields with ease. Not all fields appear in all contexts. It is generally safe to consider a nulled field, an empty set, and the absence of a field as the same thing. Please note that Tweets found in Search results vary somewhat in structure from this document.</p>
<table border="1" class="docutils">
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead valign="bottom">
<tr class="row-odd"><th class="head">Field</th>
<th class="head">Type</th>
<th class="head">Description</th>
</tr>
</thead>
<tbody valign="top">
<tr class="row-even"><td>contributors</td>


<td>Collection of Contributors</td>
<td><p class="first"><strong>Deprecated</strong> <em>Nullable</em> A collection of brief user objects (usually only one) indicating users who contributed to the
authorship of the tweet, on behalf of the official tweet author. This is a legacy value and is not actively used.</p>
<p>Example:</p>
<div class="code javascript last highlight-python"><div class="highlight"><pre><span></span>&quot;contributors&quot;:
[
    {
        &quot;id&quot;:819797,
        &quot;id_str&quot;:&quot;819797&quot;,
        &quot;screen_name&quot;:&quot;episod&quot;
    }
]
</pre></div>
</div>
</td>
</tr>



<tr class="row-odd"><td>coordinates</td>
<td><a class="reference external" href="#obj-coordinates">Coordinates</a></td>
<td><p class="first"><em>Nullable</em> Represents the geographic location of this Tweet as reported by the user or client application. The inner coordinates
array is formatted as <a class="reference external" href="http://www.geojson.org/">geoJSON</a> (longitude first, then latitude).
Example:</p>
<div class="code javascript last highlight-python"><div class="highlight"><pre><span></span>&quot;coordinates&quot;:
{
    &quot;coordinates&quot;:
    [
        -75.14310264,
        40.05701649
    ],
    &quot;type&quot;:&quot;Point&quot;
}
</pre></div>
</div>
</td>
</tr>
<tr class="row-even"><td>created_at</td>
<td>String</td>
<td><p class="first">UTC time when this Tweet was created.
Example:</p>
<div class="code javascript last highlight-python"><div class="highlight"><pre><span></span>&quot;created_at&quot;:&quot;Wed Aug 27 13:08:45 +0000 2008&quot;
</pre></div>
</div>
</td>
</tr>




<tr class="row-odd"><td>current_user_retweet</td>
<td>Object</td>
<td><p class="first"><em>Perspectival</em> Only surfaces on methods supporting the      <code class="docutils literal"><span class="pre">include_my_retweet</span></code>     parameter, when set to true. Details the
Tweet ID of the user&#8217;s own retweet (if existent) of this Tweet.
Example:</p>
<div class="code javascript last highlight-python"><div class="highlight"><pre><span></span>&quot;current_user_retweet&quot;: {
  &quot;id&quot;: 26815871309,
  &quot;id_str&quot;: &quot;26815871309&quot;
}
</pre></div>
</div>
</td>
</tr>




<tr class="row-even"><td>entities</td>
<td><a class="reference external" href="/overview/api/entities">Entities</a></td>
<td><p class="first">Entities which have been parsed out of the text of the Tweet. Additionally see <a class="reference external" href="/overview/api/entities-in-twitter-objects">Entities in Twitter
Objects</a> .
Example:</p>
<div class="code javascript last highlight-python"><div class="highlight"><pre><span></span>&quot;entities&quot;:
{
    &quot;hashtags&quot;:[],
    &quot;urls&quot;:[],
    &quot;user_mentions&quot;:[]
}
</pre></div>
</div>
</td>
</tr>






<tr class="row-odd"><td>favorite_count</td>
<td>Integer</td>
<td><p class="first"><em>Nullable</em> Indicates approximately how many times this Tweet has been  <a class="reference external" href="/rest/reference/post/favorites/create">liked</a>  by
Twitter users.
Example:</p>
<div class="code javascript last highlight-python"><div class="highlight"><pre><span></span>&quot;favorite_count&quot;:1138
</pre></div>
</div>
</td>
</tr>
<tr class="row-even"><td>favorited</td>
<td>Boolean</td>
<td><p class="first"><em>Nullable</em> <em>Perspectival</em> Indicates whether this Tweet has been liked by the authenticating user.
Example:</p>
<div class="code javascript last highlight-python"><div class="highlight"><pre><span></span>&quot;favorited&quot;:true
</pre></div>
</div>
</td>
</tr>





<tr class="row-odd"><td>filter_level</td>
<td>String</td>
<td><p class="first">Indicates the maximum value of the <a class="reference external" href="/streaming/overview/request-parameters#filter_level">filter_level</a> parameter which may be
used and still stream this Tweet. So a value of <code class="docutils literal"><span class="pre">medium</span></code> will be streamed on <code class="docutils literal"><span class="pre">none</span></code>, <code class="docutils literal"><span class="pre">low</span></code>,
and <code class="docutils literal"><span class="pre">medium</span></code> streams.</p>
<p>Example:</p>
<div class="code javascript last highlight-python"><div class="highlight"><pre><span></span>&quot;filter_level&quot;: &quot;medium&quot;
</pre></div>
</div>
</td>
</tr>
<tr class="row-even"><td>geo</td>
<td>Object</td>
<td><strong>Deprecated</strong> <em>Nullable</em> Use the <code class="docutils literal"><span class="pre">coordinates</span></code> field instead.</td>
</tr>
<tr class="row-odd"><td>id</td>
<td>Int64</td>
<td><p class="first">The integer representation of the unique identifier for this Tweet. This number is greater than 53 bits and some programming
languages may have difficulty/silent defects in interpreting it. Using a signed 64 bit integer for storing this identifier is safe.
Use      <code class="docutils literal"><span class="pre">id_str</span></code>     for fetching the identifier to stay on the safe side. See <a class="reference external" href="/overview/api/twitter-ids-json-and-snowflake">Twitter IDs, JSON and
Snowflake</a> .
Example:</p>
<div class="code javascript last highlight-python"><div class="highlight"><pre><span></span>&quot;id&quot;:114749583439036416
</pre></div>
</div>
</td>
</tr>





<tr class="row-even"><td>id_str</td>
<td>String</td>
<td><p class="first">The string representation of the unique identifier for this Tweet. Implementations should use this rather than the large integer in
<code class="docutils literal"><span class="pre">id</span></code>.
Example:</p>
<div class="code javascript last highlight-python"><div class="highlight"><pre><span></span>&quot;id_str&quot;:&quot;114749583439036416&quot;
</pre></div>
</div>
</td>
</tr>
<tr class="row-odd"><td>in_reply_to_screen_name</td>
<td>String</td>
<td><p class="first"><em>Nullable</em> If the represented Tweet is a reply, this field will contain the screen name of the original Tweet&#8217;s author.
Example:</p>
<div class="code javascript last highlight-python"><div class="highlight"><pre><span></span>&quot;in_reply_to_screen_name&quot;:&quot;twitterapi&quot;
</pre></div>
</div>
</td>
</tr>






<tr class="row-even"><td>in_reply_to_status_id</td>
<td>Int64</td>
<td><p class="first"><em>Nullable</em> If the represented Tweet is a reply, this field will contain the integer representation of the original Tweet&#8217;s ID.
Example:</p>
<div class="code javascript last highlight-python"><div class="highlight"><pre><span></span>&quot;in_reply_to_status_id&quot;:114749583439036416
</pre></div>
</div>
</td>
</tr>



<tr class="row-odd"><td>in_reply_to_status_id_str</td>
<td>String</td>
<td><p class="first"><em>Nullable</em> If the represented Tweet is a reply, this field will contain the string representation of the original Tweet&#8217;s ID.
Example:</p>
<div class="code javascript last highlight-python"><div class="highlight"><pre><span></span>&quot;in_reply_to_status_id_str&quot;:&quot;114749583439036416&quot;
</pre></div>
</div>
</td>
</tr>



<tr class="row-even"><td>in_reply_to_user_id</td>
<td>Int64</td>
<td><p class="first"><em>Nullable</em> If the represented Tweet is a reply, this field will contain the integer representation of the original Tweet&#8217;s author
ID. This will not necessarily always be the user directly mentioned in the Tweet.
Example:</p>
<div class="code javascript last highlight-python"><div class="highlight"><pre><span></span>&quot;in_reply_to_user_id&quot;:819797
</pre></div>
</div>
</td>
</tr>




<tr class="row-odd"><td>in_reply_to_user_id_str</td>
<td>String</td>
<td><p class="first"><em>Nullable</em> If the represented Tweet is a reply, this field will contain the string representation of the original Tweet&#8217;s author ID.
This will not necessarily always be the user directly mentioned in the Tweet.
Example:</p>
<div class="code javascript last highlight-python"><div class="highlight"><pre><span></span>&quot;in_reply_to_user_id_str&quot;:&quot;819797&quot;
</pre></div>
</div>
</td>
</tr>




<tr class="row-even"><td>lang</td>
<td>String</td>
<td><p class="first"><em>Nullable</em> When present, indicates a <a class="reference external" href="http://tools.ietf.org/html/bcp47">BCP 47</a> language identifier corresponding to the
machine-detected language of the Tweet text, or <code class="docutils literal"><span class="pre">und</span></code> if no language could be detected.
Example:</p>
<div class="code javascript last highlight-python"><div class="highlight"><pre><span></span>&quot;lang&quot;: &quot;en&quot;
</pre></div>
</div>
</td>
</tr>



<tr class="row-odd"><td>place</td>
<td><a class="reference external" href="/overview/api/places">Places</a></td>
<td><p class="first"><em>Nullable</em> When present, indicates that the tweet is associated (but not necessarily originating from) a
<a class="reference external" href="/overview/api/places">Place</a> .
Example:</p>
<div class="code javascript last highlight-python"><div class="highlight"><pre><span></span>&quot;place&quot;:
{
    &quot;attributes&quot;:{},
     &quot;bounding_box&quot;:
    {
        &quot;coordinates&quot;:
        [[
                [-77.119759,38.791645],
                [-76.909393,38.791645],
                [-76.909393,38.995548],
                [-77.119759,38.995548]
        ]],
        &quot;type&quot;:&quot;Polygon&quot;
    },
     &quot;country&quot;:&quot;United States&quot;,
     &quot;country_code&quot;:&quot;US&quot;,
     &quot;full_name&quot;:&quot;Washington, DC&quot;,
     &quot;id&quot;:&quot;01fbe706f872cb32&quot;,
     &quot;name&quot;:&quot;Washington&quot;,
     &quot;place_type&quot;:&quot;city&quot;,
     &quot;url&quot;: &quot;http://api.twitter.com/1/geo/id/01fbe706f872cb32.json&quot;
}
</pre></div>
</div>
</td>
</tr>





<tr class="row-even"><td>possibly_sensitive</td>
<td>Boolean</td>
<td><p class="first"><em>Nullable</em> This field only surfaces when a Tweet contains a link. The meaning of the field doesn&#8217;t pertain to the Tweet content
itself, but instead it is an indicator that the URL contained in the Tweet may contain content or media identified as sensitive
content.
Example:</p>
<div class="code javascript last highlight-python"><div class="highlight"><pre><span></span>&quot;possibly_sensitive&quot;:true
</pre></div>
</div>
</td>
</tr>



<tr class="row-odd"><td>quoted_status_id</td>
<td>Int64</td>
<td><p class="first">This field only surfaces when the Tweet is a quote Tweet. This field contains the integer value Tweet ID of the quoted Tweet.
Example:</p>
<div class="code javascript last highlight-python"><div class="highlight"><pre><span></span>&quot;quoted_status_id&quot;:114749583439036416
</pre></div>
</div>
</td>
</tr>





<tr class="row-even"><td>quoted_status_id_str</td>
<td>String</td>
<td><p class="first">This field only surfaces when the Tweet is a quote Tweet. This is the string representation Tweet ID of the quoted Tweet.
Example:</p>
<div class="code javascript last highlight-python"><div class="highlight"><pre><span></span>&quot;quoted_status_id_str&quot;:&quot;114749583439036416&quot;
</pre></div>
</div>
</td>
</tr>





<tr class="row-odd"><td>quoted_status</td>
<td><a class="reference external" href="/overview/api/tweets">Tweet</a></td>
<td>This field only surfaces when the Tweet is a quote Tweet. This attribute contains the Tweet object of the original Tweet that was
quoted.</td>
</tr>




<tr class="row-even"><td>scopes</td>
<td>Object</td>
<td><p class="first">A set of key-value pairs indicating the intended contextual delivery of the containing Tweet. Currently used by Twitter&#8217;s Promoted
Products.
Example:</p>
<div class="code javascript last highlight-python"><div class="highlight"><pre><span></span>&quot;scopes&quot;:{&quot;followers&quot;:false}
</pre></div>
</div>
</td>
</tr>





<tr class="row-odd"><td>retweet_count</td>
<td>Int</td>
<td><p class="first">Number of times this Tweet has been retweeted.
Example:</p>
<div class="code javascript last highlight-python"><div class="highlight"><pre><span></span>&quot;retweet_count&quot;:1585
</pre></div>
</div>
</td>
</tr>





<tr class="row-even"><td>retweeted</td>
<td>Boolean</td>
<td><p class="first"><em>Perspectival</em> Indicates whether this Tweet has been retweeted by the authenticating user.
Example:</p>
<div class="code javascript last highlight-python"><div class="highlight"><pre><span></span>&quot;retweeted&quot;:false
</pre></div>
</div>
</td>
</tr>



<tr class="row-odd"><td>retweeted_status</td>
<td><a class="reference external" href="/overview/api/tweets">Tweet</a></td>
<td>Users can amplify the broadcast of Tweets authored by other users by <a class="reference external" href="/rest/reference/post/statuses/retweet/%3Aid">retweeting</a> .
Retweets can be distinguished from typical Tweets by the existence of a      <code class="docutils literal"><span class="pre">retweeted_status</span></code>     attribute. This attribute
contains a representation of the <em>original</em> Tweet that was retweeted. Note that retweets of retweets do not show representations of
the intermediary retweet, but only the original Tweet. (Users can also <a class="reference external" href="/rest/reference/post/statuses/destroy/%3Aid">unretweet</a> a
retweet they created by deleting their retweet.)</td>
</tr>




<tr class="row-even"><td>source</td>
<td>String</td>
<td><p class="first">Utility used to post the Tweet, as an HTML-formatted string. Tweets from the Twitter website have a source value of <code class="docutils literal"><span class="pre">web</span></code>.</p>
<p>Example:</p>
<div class="code javascript last highlight-python"><div class="highlight"><pre><span></span>&quot;source&quot;:&quot;\u003Ca href=\&quot;http:\/\/itunes.apple.com\/us\/app\/twitter\/id409789998?mt=12\&quot; \u003ETwitter for Mac\u003C\/a\u003E&quot;
</pre></div>
</div>
</td>
</tr>




<tr class="row-odd"><td>text</td>
<td>String</td>
<td><p class="first">The actual UTF-8 text of the status update. See
<a class="reference external" href="https://github.com/twitter/twitter-text/blob/master/rb/lib/twitter-text/regex.rb">twitter-text</a> for details on what is currently
considered valid characters.
Example:</p>
<div class="code javascript last highlight-python"><div class="highlight"><pre><span></span>&quot;text&quot;:&quot;Tweet Button, Follow Button, and Web Intents javascript now support SSL http:\/\/t.co\/9fbA0oYy ^TS&quot;
</pre></div>
</div>
</td>
</tr>




<tr class="row-even"><td>truncated</td>
<td>Boolean</td>
<td><p class="first">Indicates whether the value of the      <code class="docutils literal"><span class="pre">text</span></code>     parameter was truncated, for example, as a result of a retweet exceeding the 140
character Tweet length. Truncated text will end in ellipsis, like this      <code class="docutils literal"><span class="pre">...</span></code>     Since Twitter now rejects long Tweets vs
truncating them, the large majority of Tweets will have this set to      <code class="docutils literal"><span class="pre">false</span></code>     .
Note that while native retweets may have their toplevel      <code class="docutils literal"><span class="pre">text</span></code>     property shortened, the original text will be available
under the      <code class="docutils literal"><span class="pre">retweeted_status</span></code>     object and the      <code class="docutils literal"><span class="pre">truncated</span></code>     parameter will be set to the value of the original
status (in most cases,      <code class="docutils literal"><span class="pre">false</span></code>     ).
Example:</p>
<div class="code javascript last highlight-python"><div class="highlight"><pre><span></span>&quot;truncated&quot;:true
</pre></div>
</div>
</td>
</tr>




<tr class="row-odd"><td>user</td>
<td><a class="reference external" href="/overview/api/users">Users</a></td>
<td><p class="first">The user who posted this Tweet. Perspectival attributes embedded within this object are unreliable.</p>
<p>Example:</p>
<div class="code javascript last highlight-python"><div class="highlight"><pre><span></span>&quot;user&quot;:{&quot;statuses_count&quot;:3080, &quot;favourites_count&quot;:22, &quot;protected&quot;:false, &quot;profile_text_color&quot;:&quot;437792&quot;, &quot;profile_image_url&quot;:&quot;...&quot;
&quot;profile_image_url&quot;:&quot;...&quot;, &quot;name&quot;:&quot;Twitter API&quot;, &quot;profile_sidebar_fill_color&quot;:&quot;a9d9f1&quot;, &quot;listed_count&quot;:9252, &quot;following&quot;:true,
&quot;profile_background_tile&quot;:false, &quot;utc_offset&quot;:-28800,
&quot;description&quot;:&quot;The Real Twitter API. I tweet about API changes. Don&#39;t get an answer? It&#39;s on my website.&quot;,
&quot;location&quot;:&quot;San Francisco, CA&quot;, &quot;contributors_enabled&quot;:true, &quot;verified&quot;:true, &quot;profile_link_color&quot;:&quot;0094C2&quot;,
&quot;followers_count&quot;:665829, &quot;url&quot;:&quot;http:\/\/dev.twitter.com&quot;, &quot;default_profile&quot;:false, &quot;profile_sidebar_border_color&quot;:&quot;0094C2&quot;,
&quot;screen_name&quot;:&quot;twitterapi&quot;, &quot;default_profile_image&quot;:false, &quot;notifications&quot;:false, &quot;display_url&quot;:null,
&quot;show_all_inline_media&quot;:false, &quot;geo_enabled&quot;:true, &quot;profile_use_background_image&quot;:true, &quot;friends_count&quot;:32, &quot;id_str&quot;:&quot;6253282&quot;,
&quot;entities&quot;:{&quot;hashtags&quot;:[], &quot;urls&quot;:[], &quot;user_mentions&quot;:[]}, &quot;expanded_url&quot;:null, &quot;is_translator&quot;:false, &quot;lang&quot;:&quot;en&quot;,
&quot;time_zone&quot;:&quot;Pacific Time (US &amp; Canada)&quot;, &quot;created_at&quot;:&quot;Wed May 23 06:01:13 +0000 2007&quot;, &quot;profile_background_color&quot;:&quot;e8f2f7&quot;,
&quot;id&quot;:6253282, &quot;follow_request_sent&quot;:false, &quot;profile_background_image_url_https&quot;:&quot;...&quot;, &quot;profile_background_image_url&quot;:&quot;...&quot;,}
</pre></div>
</div>
</td>
</tr>



<tr class="row-even"><td>withheld_copyright</td>
<td>Boolean</td>
<td><p class="first">When present and set to &#8220;true&#8221;, it indicates that this piece of content has been withheld due to a <a class="reference external" href="http://en.wikipedia.org/wiki/Digital_Millennium_Copyright_Act">DMCA
complaint</a> .
Example:</p>
<div class="code javascript last highlight-python"><div class="highlight"><pre><span></span>&quot;withheld_copyright&quot;: true
</pre></div>
</div>
</td>
</tr>




<tr class="row-odd"><td>withheld_in_countries</td>
<td>Array of String</td>
<td><p class="first">When present, indicates a list of uppercase <a class="reference external" href="http://en.wikipedia.org/wiki/ISO_3166-1_alpha-2">two-letter country codes</a> this
content is withheld from. Twitter supports the following non-country values for this field:</p>
<p>&#8220;XX&#8221; - Content is withheld in all countries
&#8220;XY&#8221; - Content is withheld due to a DMCA request.</p>
<p>Example:</p>
<div class="code javascript last highlight-python"><div class="highlight"><pre><span></span>&quot;withheld_in_countries&quot;: [&quot;GR&quot;, &quot;HK&quot;, &quot;MY&quot;]
</pre></div>
</div>
</td>
</tr>




<tr class="row-even"><td>withheld_scope</td>
<td>String</td>
<td><p class="first">When present, indicates whether the content being withheld is the &#8220;status&#8221; or a &#8220;user.&#8221;</p>
<p>Example:</p>
<div class="code javascript last highlight-python"><div class="highlight"><pre><span></span>&quot;withheld_scope&quot;: &quot;status&quot;
</pre></div>
</div>
</td>
</tr>
</tbody>
</table>




<div class="section" id="coordinates">
<h3>Coordinates<a class="headerlink" href="#coordinates" title="Permalink to this headline">¶</a></h3>
<table border="1" class="docutils">
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<tbody valign="top">
<tr class="row-odd"><td>Field</td>
<td>Type</td>
<td>Description</td>
</tr>
<tr class="row-even"><td>coordinates</td>
<td>Collection of Float</td>
<td><p class="first">The longitude and latitude of the Tweet&#8217;s location, as a collection in the form [longitude, latitude].
Example:</p>
<div class="code javascript last highlight-python"><div class="highlight"><pre><span></span>&quot;coordinates&quot;:[-97.51087576,35.46500176]
</pre></div>
</div>
</td>
</tr>
<tr class="row-odd"><td>type</td>
<td>String</td>
<td><p class="first">The type of data encoded in the coordinates property. This will be &#8220;Point&#8221; for Tweet coordinates fields.
Example:</p>
<div class="code javascript last highlight-python"><div class="highlight"><pre><span></span>&quot;type&quot;: &quot;Point&quot;
</pre></div>
</div>
</td>
</tr>
</tbody>
</table>
</div>
</div>
</div>


  