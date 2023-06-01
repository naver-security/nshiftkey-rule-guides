---
title: ""
category: ""
order: 0
---

<h1>"&lt;strong&gt;" and "&lt;em&gt;" tags should be used</h1>
<small>Web:BoldAndItalicTagsCheck</small>
<br>
<p>The <code>&lt;strong&gt;</code>/<code>&lt;b&gt;</code> and <code>&lt;em&gt;</code>/<code>&lt;i&gt;</code> tags have exactly the same effect in most
web browsers, but there is a fundamental difference between them: <code>&lt;strong&gt;</code> and <code>&lt;em&gt;</code> have a semantic meaning
whereas <code>&lt;b&gt;</code> and <code>&lt;i&gt;</code> only convey styling information like CSS.</p>
<p>While <code>&lt;b&gt;</code> can have simply no effect on a some devices with limited display or when a screen reader software is used by a blind
person, <code>&lt;strong&gt;</code> will:</p>
<ul>
  <li> Display the text bold in normal browsers </li>
  <li> Speak with lower tone when using a screen reader such as Jaws </li>
</ul>
<p>Consequently:</p>
<ul>
  <li> in order to convey semantics, the <code>&lt;b&gt;</code> and <code>&lt;i&gt;</code> tags shall never be used, </li>
  <li> in order to convey styling information, the <code>&lt;b&gt;</code> and <code>&lt;i&gt;</code> should be avoided and CSS should be used instead.
  </li>
</ul>
<h2>Noncompliant Code Example</h2>
<pre>
&lt;i&gt;car&lt;/i&gt;             &lt;!-- Noncompliant --&gt;
&lt;b&gt;train&lt;/b&gt;         &lt;!-- Noncompliant --&gt;
</pre>
<h2>Compliant Solution</h2>
<pre>
&lt;em&gt;car&lt;/em&gt;
&lt;strong&gt;train&lt;/strong&gt;
</pre>
<h2>Exceptions</h2>
<p>This rule is relaxed in case of <a href="https://www.w3.org/WAI/GL/wiki/Using_aria-hidden%3Dtrue_on_an_icon_font_that_AT_should_ignore">icon
fonts</a> usage.</p>
<pre>
&lt;i class="..." aria-hidden="true" /&gt;    &lt;!-- Compliant icon fonts usage --&gt;
</pre>