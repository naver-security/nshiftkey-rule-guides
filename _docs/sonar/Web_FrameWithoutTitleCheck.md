---
title: ""
category: ""
order: 0
---

<h1>"&lt;frames&gt;" should have a "title" attribute</h1>
<small>Web:FrameWithoutTitleCheck</small>
<br>
<p>Frames allow different web pages to be put together on the same visual space. Users without disabilities can easily scan the contents of all frames
at once. However, visually impaired users using screen readers hear the page content linearly.</p>
<p>The <code>title</code> attribute is used to list all the page’s frames, enabling those users to easily navigate among them. Therefore, the
<code>&lt;frame&gt;</code> and <code>&lt;iframe&gt;</code> tags should always have a <code>title</code> attribute.</p>
<h2>Noncompliant Code Example</h2>
<pre>
&lt;frame src="index.php?p=menu"&gt;                                      &lt;-- Non-Compliant --&gt;
&lt;frame src="index.php?p=home" name="contents"&gt;                      &lt;-- Non-Compliant --&gt;
</pre>
<h2>Compliant Solution</h2>
<pre>
&lt;frame src="index.php?p=menu" title="Navigation menu"&gt;              &lt;-- Compliant --&gt;
&lt;frame src="index.php?p=home" title="Main content" name="contents"&gt; &lt;-- Compliant --&gt;
</pre>