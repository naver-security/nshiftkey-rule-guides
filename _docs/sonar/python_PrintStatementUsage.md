---
title: ""
category: ""
order: 0
---

<h1>The "print" statement should not be used</h1>
<small>python:PrintStatementUsage</small>
<br>
<p>The <code>print</code> statement was removed in Python 3.0. The built-in function should be used instead.</p>
<h2>Noncompliant Code Example</h2>
<pre>
print '1'  # Noncompliant
</pre>
<h2>Compliant Solution</h2>
<pre>
print('1')
</pre>