---
title: ""
category: ""
order: 0
---

<h1>The "exec" statement should not be used</h1>
<small>python:ExecStatementUsage</small>
<br>
<p>Use of the <code>exec</code> statement could be dangerous, and should be avoided. Moreover, the <code>exec</code> statement was removed in Python
3.0. Instead, the built-in <code>exec()</code> function can be used.</p>
<h2>Noncompliant Code Example</h2>
<pre>
exec 'print 1' # Noncompliant
</pre>
<h2>Compliant Solution</h2>
<pre>
exec('print 1')
</pre>