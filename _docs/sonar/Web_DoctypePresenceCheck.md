---
title: ""
category: ""
order: 0
---

<h1>"&lt;!DOCTYPE&gt;" declarations should appear before "&lt;html&gt;" tags</h1>
<small>Web:DoctypePresenceCheck</small>
<br>
<p>The <code>&lt;!DOCTYPE&gt;</code> declaration tells the web browser which (X)HTML version is being used on the page, and therefore how to interpret
the various elements.</p>
<p>Validators also rely on it to know which rules to enforce.</p>
<p>It should always preceed the <code>&lt;html&gt;</code> tag.</p>
<h2>Noncompliant Code Example</h2>
<pre>
&lt;html&gt;  &lt;!-- Noncompliant --&gt;
...
&lt;/html&gt;
</pre>
<h2>Compliant Solution</h2>
<pre>
&lt;!DOCTYPE html&gt;
&lt;html&gt;  &lt;!-- Compliant --&gt;
...
&lt;/html&gt;
</pre>