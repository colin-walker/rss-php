# Fork change notes

- fromRSS & fromAtom function changed from private to public so they can be called directly: e.g. `$rss = Feed::fromRss($xml);`

This let's you use curl_multi to fetch a group of feeds, convert them to a SimpleXMLElement and pass that straight to the functions. This saves considerable time when fetching multiple feeds.

- added support for unrecognised namespaces

Checks have been added for the ['source' namespace](http://source.scripting.com/) by Dave Winer (specifically to detect `<source:markdown>` elements) and the ['now' namespace](https://nowns.work). The 'now' namespace is my own proposal for sharing /now page style updates via RSS.

**Markdown**

```
$rss = Feed::fromRss($xml);

foreach ($rss->item as $item) {
  $markdown = $item->markdown;
}
```

**now elements**

```
$rss = Feed::fromRss($xml);

$nowTitle = addslashes($rss->nowTitle);
$nowLink = $rss->nowLink;
$nowContent = addslashes($rss->nowContent);
$nowMarkdown = addslashes($rss->nowMarkdown);
$nowTimestamp = $rss->nowTimestamp;
```

- added support for JSONfeed

Integrated the code from [AnTheMaker's PR](https://github.com/dg/rss-php/pull/21) to the original repo.