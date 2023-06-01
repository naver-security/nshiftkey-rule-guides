---
title: ""
category: ""
order: 0
---

<h1>Backticks should not be used</h1>
<small>python:BackticksUsage</small>
<br>
<p>Backticks are a deprecated alias for <code>repr()</code>. Don’t use them any more, the syntax was removed in Python 3.0.</p>
<h2>Noncompliant Code Example</h2>
<pre>
return `num`  # Noncompliant
</pre>
<h2>Compliant Solution</h2>
<pre>
return repr(num)
</pre>