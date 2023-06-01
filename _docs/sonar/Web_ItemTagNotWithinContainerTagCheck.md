---
title: ""
category: ""
order: 0
---

<h1>"&lt;li&gt;" and "&lt;dt&gt;" item tags should be in "&lt;ul&gt;", "&lt;ol&gt;" or "&lt;dl&gt;" container tags</h1>
<small>Web:ItemTagNotWithinContainerTagCheck</small>
<br>
<p>Using a <code>&lt;li&gt;</code> or <code>&lt;dt&gt;</code> item tag outside of a <code>&lt;ul&gt;</code>, <code>&lt;ol&gt;</code> or
<code>&lt;dl&gt;</code> one does not make sense and indicates a bug.</p>
<h2>Noncompliant Code Example</h2>
<pre>
&lt;li&gt;Apple&lt;/li&gt;          &lt;!-- Noncompliant --&gt;
&lt;li&gt;Strawberry&lt;/li&gt;     &lt;!-- Noncompliant --&gt;

&lt;li&gt;Apple&lt;/li&gt;          &lt;!-- Noncompliant --&gt;
&lt;li&gt;Strawberry&lt;/li&gt;     &lt;!-- Noncompliant --&gt;

&lt;dt&gt;Apple&lt;/dt&gt;          &lt;!-- Noncompliant --&gt;
&lt;dt&gt;Strawberry&lt;/dt&gt;     &lt;!-- Noncompliant --&gt;
</pre>
<h2>Compliant Solution</h2>
<pre>
&lt;ul&gt;
  &lt;li&gt;Apple&lt;/li&gt;
  &lt;li&gt;Strawberry&lt;/li&gt;
&lt;/ul&gt;

&lt;ol&gt;
  &lt;li&gt;Apple&lt;/li&gt;
  &lt;li&gt;Strawberry&lt;/li&gt;
&lt;/ol&gt;

&lt;dl&gt;
  &lt;dt&gt;Apple&lt;/dt&gt;
  &lt;dt&gt;Strawberry&lt;/dt&gt;
&lt;/dl&gt;
</pre>