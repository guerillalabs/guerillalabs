---
layout: blog
title: Sass Extends with Media Queries
author: Jacob Fentress
categories: Blog
tags: [ blog, rss, sass ]
css: screen
code: true
---

Here at Guerilla Labs, we use Sass *a lot*. Often, I'll define some silent classes like:

<pre><code class="language-css">%vertical-margin-l {
    margin-bottom: 48px;
}
%vertical-margin-m {
    margin-bottom: 40px;
}
%vertical-margin-s {
    margin-bottom: 32px;
}</code></pre>

Then, while defining a module, I would like to do something like:

<pre><code class="language-css">.module {
    @extends %vertical-margin-s;

    @media (min-width: 400px) {
        @extends %vertical-margin-m;
    }
    @media (min-width: 600px) {
        @extends %vertical-margin-l;
    }
}</code></pre>

But Sass doesn't like that and won't allow you to perform an <code class="language-css">@extends</code> from within a media query.

Fortunately, there is another way because the extended silent class can have media queries, which then carry over to the extending element. So, do this instead:

 <pre><code class="language-css">%vertical-margin-l {
    margin-bottom: 32px;

    @media (min-width: 400px) {
        margin-bottom: 40px;
    }
    @media (min-width: 600px) {
        margin-bottom: 48px;
    }
}

.module {
    @extends %vertical-margin-l;
}</code></pre>

You'll gain the extra benefit of keeping your code DRYer, though you'll need to more carefully consider how you structure your silent classes.

We use this trick for all spacing and font-sizing throughout most of our projects. Enjoy.