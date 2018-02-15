---
layout: post
summary: "Google 2016 update for JS sites"
tags: programming seo google
---
> Source: [John Mueller](https://plus.google.com/+JohnMueller/posts/LT4fU7kFB8W) in [Search engines & websites!](https://plus.google.com/collection/oSHR9) collection on Google+ 

An update (March 2016) on the current state & recommendations for JavaScript sites / [Progressive Web Apps][1] in Google Search. We occasionally see questions about what JS-based sites can do and still be visible in search, so here's a brief summary for today's state:

- Don't cloak to Googlebot. Use "feature detection" & "[progressive enhancement][2]"
- Use [rel=canonical][3] when serving content from multiple URLs is required.
- Avoid the [AJAX-Crawling scheme][4] on new sites
- Avoid using `#` in URLs (outside of `#!`)
- Use [Search Console's Fetch and Render tool][5] to test how Googlebot sees your pages
- Ensure that all required resources (including JavaScript files / frameworks, server responses, 3rd-party APIs, etc) aren't blocked by `robots.txt`
- Limit the number of embedded resources, in particular the number of JavaScript files and server responses required to render your page
- Google supports the use of JavaScript to provide titles, description & robots meta tags, structured data, and other meta-data
- Finally, keep in mind that other search engines and web services accessing your content might not support JavaScript at all, or might support a different subset. 

[1]: https://developers.google.com/web/progressive-web-apps
[2]: https://en.wikipedia.org/wiki/Progressive_enhancement
[3]: https://support.google.com/webmasters/answer/139066
[4]: https://developers.google.com/webmasters/ajax-crawling/docs/specification
[5]: https://support.google.com/webmasters/answer/6066468﻿
