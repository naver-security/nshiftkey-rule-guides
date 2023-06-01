---
title: ""
category: ""
order: 0
---

<h1>"&lt;title&gt;" should be present in all pages</h1>
<small>Web:PageWithoutTitleCheck</small>
<br>
<p>Titles are important because they are displayed in search engine results as well as the browser’s toolbar.</p>
<p>This rule verifies that the <code>&lt;head&gt;</code> tag contains a <code>&lt;title&gt;</code> one, and the <code>&lt;html&gt;</code> tag a
<code>&lt;head&gt;</code> one.</p>
<h2>Noncompliant Code Example</h2>
<pre>
&lt;html&gt;         &lt;!-- Non-Compliant --&gt;

&lt;body&gt;
...
&lt;/body&gt;

&lt;/html&gt;
</pre>
<h2>Compliant Solution</h2>
<pre>
&lt;html&gt;         &lt;!-- Compliant --&gt;

&lt;head&gt;
&lt;title&gt;Some relevant title&lt;/title&gt;
&lt;/head&gt;

&lt;body&gt;
...
&lt;/body&gt;

&lt;/html&gt;
</pre>