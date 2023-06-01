---
title: ""
category: ""
order: 0
---

<h1>"&lt;&gt;" should not be used to test inequality</h1>
<small>python:InequalityUsage</small>
<br>
<p>The forms <code>&lt;&gt;</code> and <code>!=</code> are equivalent. But in Python 2.7.3 the <code>&lt;&gt;</code> form is considered obsolete.</p>
<h2>Noncompliant Code Example</h2>
<pre>
return a &lt;&gt; b # Noncompliant
</pre>
<h2>Compliant Solution</h2>
<pre>
return a != b
</pre>