---
layout: post
title:  "調整さま: 調整さんのUI改善ブックマークレット"
date:   2014-02-18 22:09:29
categories: productivity
---

# 調整さんを使いやすくしよう

[調整さん][chouseisan]、アカウント登録無しでお手軽に使えて便利ですよね。
でも1つだけどうしても許せないことがあります。それは、

__◯△☓の選択がドロップダウンメニューなこと。__

なぜここで2回もクリックしなくてはならないのか。
私の人生をこんなとこで無駄遣いする訳にはいきません。

ということで、改善するブックマークレットを書きました
(ブックマークレットの使い方は[こちら][howtousebookmarklet])。

<a class="button" href="javascript:(function(e,a,g,h,f,c,b,d){if(!(f=e.jQuery)||g&gt;f.fn.jquery||h(f)){c=a.createElement(&quot;script&quot;);c.type=&quot;text/javascript&quot;;c.src=&quot;http://ajax.googleapis.com/ajax/libs/jquery/&quot;+g+&quot;/jquery.min.js&quot;;c.onload=c.onreadystatechange=function(){if(!b&amp;&amp;(!(d=this.readyState)||d==&quot;loaded&quot;||d==&quot;complete&quot;)){h((f=e.jQuery).noConflict(1),b=1);f(c).remove()}};a.documentElement.childNodes[0].appendChild(c)}})(window,document,&quot;1.6.1&quot;,function($,L){jQuery(function(a){return a(&quot;form#f select&quot;).each(function(){var c,d,e,b;b=a(this);d=a(&quot;&lt;a&gt;\u25cb&lt;/a&gt;&quot;).css(&quot;margin&quot;,&quot;0 5px&quot;);e=a(&quot;&lt;a&gt;\u25b3&lt;a&gt;&quot;).css(&quot;margin&quot;,&quot;0 5px&quot;);c=a(&quot;&lt;a&gt;\u00d7&lt;a&gt;&quot;).css(&quot;margin&quot;,&quot;0 5px&quot;);d.bind(&quot;click&quot;,function(){return b.val(&quot;\u25cb&quot;)});e.bind(&quot;click&quot;,function(){return b.val(&quot;\u25b3&quot;)});c.bind(&quot;click&quot;,function(){return b.val(&quot;\u00d7&quot;)});return b.parent().append(d,e,c)})});});">調整さま</a>

Before:

{% image chouseisama-before.png %}

After:

{% image chouseisama-after.png %}

ちなみにコードはこんな感じです:

{% highlight ruby %}
jQuery ($) ->
  $('form#f select').each ->
    select = $(this)

    good = $('<a>○</a>').css('margin', '0 5px')
    maybe = $('<a>△<a>').css('margin', '0 5px')
    bad = $('<a>×<a>').css('margin', '0 5px')
    good.bind 'click', ->
      select.val('○')
    maybe.bind 'click', ->
      select.val('△')
    bad.bind 'click', ->
      select.val('×')

    select.parent().append good, maybe, bad
{% endhighlight %}

これを [CoffeeMarklet][coffeemarklet] でブックマークレットにしました。

# What's Next?

「ブックマークレットをクリックするのがめんどくさい」という方(素晴らしい！)には、
[dotjs][dotjs] がおすすめです。

[chouseisan]: http://chouseisan.com/
[howtousebookmarklet]: http://www.lifehacker.jp/2013/04/130402bookmarklet_matome.html
[coffeemarklet]: http://johtso.github.io/CoffeeMarklet/
[dotjs]: https://github.com/defunkt/dotjs
