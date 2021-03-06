---
layout: post
title: "Tracking Knowledge Base Articles with Google Analytics"
date: 2013-05-24 12:30
comments: true
categories: [insights, analytics]
---

Basic analytics these days: put Google's Javascript snippet on your website and you're pretty much set. Every visit gets logged. But what if you want to track something specific? This is by no means an article on super advanced Google Analytics Wizardry, but a short recount of how I took the time to make Google Analytics work for me, and people using my apps.

<!-- more -->

I use [Uservoice](http://uservoice.com) to manage tickets for Porthole, AirVLC and [other Danger Cove apps](http://dangercove.com). While doing helpdesk, I usually notice that some questions get asked more than once. That's when I try to wrap the answer in a [knowledge base article](http://porthole.uservoice.com/knowledgebase). First and foremost because it will help people out even faster than I can respond via email. Questions like: "Will this work on my Mac?" and "If I buy Porthole, how will I get it?" are perfect for a knowledge base entry. The answer is similar for everyone and it's something that you want to know _now_, instead of in an hour. The huge downside however, is that I don't get the chance to interact with my customer. This goes double for questions that have similar solutions for everyone, but when asked a lot might indicate an underlying problem that could be fixed in an update.

This means that when the knowledge base expands, I need a way to track how often each article is read. Seeing the amount of support calls drop (good), but not knowing when everybody encounters the same problem and silently discards your app (pretty bad) is a _very_ uncomfortable feeling. Trust me. Uservoice has some built-in analytics that provide general statistics, but because I chose to [show knowledge base articles on the product pages](http://getporthole.coms/upport) as well, I need something extra.

![Click on the title to unfold the full article](/assets/blog/uservoice/porthole-support.png)

The embedded knowledge base shows each article's title, clicking it will unfold the answer. Much like you see on countless other sites. The only thing I need is an overview of which of these titles get clicked most. Easy right? It _is_ actually. [Events](https://developers.google.com/analytics/devguides/collection/gajs/eventTrackerGuide) make this ridiculously straight forward. Trigger an event and it will show up in Google Analytics, [even in real-time](http://techcrunch.com/2013/03/28/google-analytics-real-time-stats-now-feature-event-reports-device-breakdown-and-shortcuts/). This is what it looks like in Javascript.

```javascript
_gaq.push(['_trackEvent', 'Support', 'Open article_107729', 'article_107729']);
```

Or if you prefer to make the call inline.

```javascript
<a href="#" onclick="_gaq.push(['_trackEvent', 'Support', 'Open article_107729', 'article_107729']);">Article title</a>
```

These events fire every time someone opens (or closes; I log that separately) an article.

![Overview of the  most popular knowledge base article](/assets/blog/uservoice/porthole-support-overview.jpg)

What I end up with is a nice overview of which topics get consulted the most! This still doesn't beat communicating via email, but it makes sure that I can at least determine where to focus my attention (and sleep at night).
