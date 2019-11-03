---
layout: post
title: "Header Bidding implementation email"
categories: [javascript, implementation]
date: 2014-01-01
---
**Project**: Header Bidder implementation email<br/>
**Company**: AudienceScience

Hi _____,

Below are links to the implementation guide. *[Deleted.]*

The remainder of this email is a quick start guide to facilitate your implementation. The following placement IDs have been set up for your creative sizes and can be found in the tags below:

**728x90 Placement ID**: `123abc` <br/>
**300x250 Placement ID**: `987zyx`
<br/><br/>

<h2>Quick Start</h2>

1. Add the following **Pre-Qualification (PreQual)** tag to the top of your webpages.
{% highlight html linenos%}
<script type="text/javascript" language="JavaScript"> 
var cb = new Date().getTime(); 
var asiPqTag = false; 
try {
   document.write("<sc" + "ript type='text/javascript' language='JavaScript' src='//pq-direct.revsci.net/pql?placementIdList=123abc,987zyx&cb=" + cb + "'></sc" + "ript>");
} catch(err) { }  
</script>
{% endhighlight %}
2. Directly after the PreQual tag, add the following **Publisher Ad Server Integration Tag (PASIT)**. This should be used in place of the tag that is listed in the attached integration guide.
{% highlight html linenos%}
<script type="text/javascript" language="JavaScript"> 
if (typeof asiPlacements != "undefined") { for(var p in asiPlacements) {
   window["ASPQ_"+p]=""; for(var key in asiPlacements[p].data) {
      window["ASPQ_"+p] += "PQ_"+p+"_"+key;       
   }    
}
</script>
{% endhighlight %}
<p>This script above reformats the recommendations for your ad call. Specifically, it defines <strong>ASPQ_<em>placementID</em></strong> variables with <strong>PQ_<em>placementID_LineItemID</em></strong>.</p>
</li>
<li>Next, amend your ad calls in a manner similar to the following example for 728x90:
<pre><code>"http://adserver.adtechus.com/addyn/3.0/5214.1/2468246/0/-1/ADTECH;loc=100;Alias=cool_location_onpage_728x90_2;%20Size=728x90;%20KV=;target=_blank;key=;grp=148;' + ASPQ_123abc  + ';misc=1412701805995;aduho=-420;rdclick="</code></pre>
<p>The output example should look like this:</p>
<pre><code>http://adserver.adtechus.com/addyn/3.0/5214.1/2468246/0/-1/ADTECH;loc=100;Alias=cool_location_onpage_728x90_2;%20Size=728x90;%20KV=;target=_blank;key=;grp=148;gwd=PQ_123abc_XXAU-li001;misc=1412701805995;aduho=-420;rdclick=</code></pre>
</li>
<li>Next, apply key and value targeting to the line items trafficked in your ad server. For every live campaign, the key and value pair will be different and will be provided to you by our Platform team. For this implementation test, please use the following key and value pairs:
<pre>   <strong>For 728x90 use</strong>:  PQ_123abc_XXAU-li001
   <strong>For 300x250 use:</strong> PQ_987zyx_XXAU-li002</pre>
</li>
<li>Finally, use the following creative tags for all display line items trafficked in your ad server (the remaining tags can be found in the attached XLS file):<br /><strong>728x90</strong>
<pre class="line-numbers"><code class="language-javascript">&lt;script type="text/javascript" language="JavaScript"&gt;
var asiPlacements = asiPlacements || top.asiPlacements;
var asiAdserver = asiAdserver || top.asiAdserver;
document.write('&lt;scri'+'pt type="text/javascript" src="//' + asiAdserver + '/rtbads/pq?mode=s&amp;placement=123abc&amp;adgroup=' + asiPlacements['123abc']['default'].key + '&amp;blob=' + asiPlacements['123abc'].blob + '&amp;cachebuster=[CACHEBUSTER]&amp;click=[CLICKTRACKER]"&gt;&lt;/scri'+'pt&gt;');
&lt;/script&gt;</code></pre>
<p> </p>
<p><strong>300x250</strong></p>
<pre class="line-numbers"><code class="language-javascript">&lt;script type="text/javascript" language="JavaScript"&gt;
var asiPlacements = asiPlacements || top.asiPlacements;
var asiAdserver = asiAdserver || top.asiAdserver;
document.write('&lt;scri'+'pt type="text/javascript" src="//' + asiAdserver + '/rtbads/pq?mode=s&amp;placement=987zyx&amp;adgroup=' + asiPlacements['987zyx']['default'].key + '&amp;blob=' + asiPlacements['987zyx'].blob + '&amp;cachebuster=[CACHEBUSTER]&amp;click=[CLICKTRACKER]"&gt;&lt;/scri'+'pt&gt;');
</code></pre>
</li>
</ol>
