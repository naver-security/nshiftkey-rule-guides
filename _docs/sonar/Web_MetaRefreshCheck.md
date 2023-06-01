---
title: ""
category: ""
order: 0
---

<h1>Meta tags should not be used to refresh or redirect</h1>
<small>Web:MetaRefreshCheck</small>
<br>
<p>Use of <code>&lt;meta http-equiv="refresh"&gt;</code> is discouraged by the World Wide Web Consortium (W3C).</p>
<p>If a user clicks the 'Back' button, some browers will go back to the redirecting page, which will prevent the user from actually going back.</p>
<p>To refresh the page, a better alternative is to use Ajax, to refresh only what needs to be refreshed and not the whole page.</p>
<p>To redirect to another page, using the HTTP response status code 301 'Moved Permanently' and 302 'Found' is a better option.</p>
<h2>Noncompliant Code Example</h2>
<pre>
&lt;head&gt;
  &lt;meta http-equiv="refresh" content="5"&gt;   &lt;!-- Non-Compliant --&gt;
  &lt;meta name="description" content="..."&gt;
&lt;/head&gt;
</pre>
<h2>Compliant Solution</h2>
<pre>
&lt;head&gt;
  &lt;meta name="description" content="..."&gt;
&lt;/head&gt;
</pre>