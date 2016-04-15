# Social Mention API Documentation #

Social Mention provides an API for developers query for social media search results in several different formats.

## Search API ##

The search API provides a single stream of real-time search data aggregated from numerous social media properties. It is available in several formats.

**Base URL prefix:**
```
http://socialmention.com/search
```
**REST Parameters:**
| **Parameter** | **Description** |
|:--------------|:----------------|
|q              |url encoded query terms (can include exception ex: "iphone apps -blackberry")|
|f              | response format (json, php, xml, rss, csv)|
|t`[]`          | search type (blogs, microblogs, bookmarks, comments, events, images, news, videos, audio, questions, networks, all), can use multiple ex: http://socialmention.com/search?q=iphone&t[]=blogs&t[]=microblogs|
|src`[]`        | (optional) specific social media sources (ex: http://socialmention.com/search?q=iphone&src[]=twitter&t[]=youtube) |
|lang           | (optional) 2 letter [ISO 639-1](http://en.wikipedia.org/wiki/ISO_639-1) language code (if null - source default language will be returned|
|strict         | (default true) disable strict mode, which will not query sources that do not support the language param (true, false)|
|l              | location string (city and state/province). Required if search type is "events"|
|callback       | (optional) required for JSONP compatible requests|
|key            | (optional) required for commercial requests|
|from\_ts       | (optional) remove results older than the supplied number of seconds, ex: to remove results older than 1 day &from\_ts=86400  |
|meta`[]`       | (optional) meta data to include, ex: &meta[.md](.md)=top |

**Example:**
```
http://socialmention.com/search?q=iphone+apps&f=json&t=microblogs&lang=fr
```

### Response Properties ###
The search API will return the following properties for JSON, PHP, and XML response formats. NOTE: Not all metadata is available for every item.

  * title - title of search
  * timestamp - search timestamp
  * count - number of items
  * items (array)
    * id - unique hash id based on url (datatype INT 20)
    * title
    * description
    * link
    * timestamp
    * language - language code
    * image - story or item image
    * embed - video embed script
    * user - author's username
    * user\_image - author's profile image
    * user\_link - author's profile url
    * domain - the original source's domain
    * source - the original source's name
    * favicon - the original source's favicon
    * type - mention type, ie: blogs, microblogs, comments etc.

Additional item properties (available to commercial API users):

  * sentiment - positive or negative integer score, ex: -1, 0, +8 etc.
  * retweet - is mention a retweet, boolean, ex: "RT @..."
  * urls\_cited - number of links in mention
  * hashtags - number of hashtags in mention, ex: "... #hashtag"
  * references - number of @references in mention
  * top\_users - array of top users by activity
  * top\_hashtags - array of top hashtags
  * top\_keywords - array of top keywords