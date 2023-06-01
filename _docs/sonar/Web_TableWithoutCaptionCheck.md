---
title: ""
category: ""
order: 0
---

<h1>"&lt;table&gt;" tags should have a description</h1>
<small>Web:TableWithoutCaptionCheck</small>
<br>
<p>In order to be accessible to visually impaired users, it is important that tables provides a description of its content before the data is
accessed.</p>
<p>The simplest way to do it, and also the one <a href="https://www.w3.org/TR/WCAG20-TECHS/H39">recommended by WCAG2</a> is to add a
<code>&lt;caption&gt;</code> element inside the <code>&lt;table&gt;</code>.</p>
<p>Other technics this rule accepts are:</p>
<ul>
  <li> adding a concise description via <a href="https://www.w3.org/TR/wai-aria/#aria-label"><code>aria-label</code></a> or <a
  href="https://www.w3.org/TR/wai-aria/#aria-labelledby"><code>aria-labelledby</code></a> attributes in the <code>&lt;table&gt;</code>. </li>
  <li> referencing a description element with an <a href="https://www.w3.org/TR/wai-aria/#aria-describedby"><code>aria-describedby</code></a>
  attribute in the <code>&lt;table&gt;</code>. </li>
  <li> embedding the <code>&lt;table&gt;</code> inside a <code>&lt;figure&gt;</code> which also contains a <code>&lt;figcaption&gt;</code>. </li>
  <li> adding a <code>summary</code> attribute to the <code>&lt;table&gt;</code> tag. However note that this attribute has been deprecated in HTML5.
  </li>
</ul>
<p>See&nbsp;<a href="https://www.w3.org/WAI/tutorials/tables/tips/">W3C WAI&nbsp;Web Accessibility Tutorials</a>&nbsp;for more information.</p>
<p>This rule raises an issue when a <code>&lt;table&gt;</code> has neither of the previously mentioned description mechanisms.</p>
<h2>Noncompliant Code Example</h2>
<pre>
&lt;table&gt; &lt;!-- Noncompliant --&gt;
  ...
&lt;table&gt;
</pre>
<h2>Compliant Solution</h2>
<p>Adding a <code>&lt;caption&gt;</code> element.</p>
<pre>
&lt;table&gt;
  &lt;caption&gt;New York City Marathon Results 2013&lt;/caption&gt;
  ...
&lt;/table&gt;
</pre>
<p>Adding an <code>aria-describedby</code> attribute.</p>
<pre>
&lt;p id="mydesc"&gt;New York City Marathon Results 2013&lt;/p&gt;
&lt;table aria-describedby="mydesc"&gt;
  ...
&lt;/table&gt;
</pre>
<p>Embedding the table in a <code>&lt;figure&gt;</code> which also contains a <code>&lt;figcaption&gt;</code>.</p>
<pre>
&lt;figure&gt;
  &lt;figcaption&gt;New York City Marathon Results 2013&lt;/figcaption&gt;
  &lt;table&gt;
    ...
  &lt;/table&gt;
&lt;/figure&gt;
</pre>
<p>Adding a <code>summary</code> attribute.&nbsp;However note that this attribute has been deprecated in HTML5.</p>
<pre>
&lt;table summary="New York City Marathon Results 2013"&gt;
  ...
&lt;/table&gt;
</pre>
<h2>Exceptions</h2>
<p>No issue will be raised on <code>&lt;table&gt;</code> used for layout purpose, i.e. when it contains a <code>role</code> attribute set to
<code>"presentation"</code> or <code>"none"</code>. Note that using <code>&lt;table&gt;</code> for layout purpose is a bad practice.</p>
<p>No issue will be raised either on <code>&lt;table&gt;</code> containing an <code>aria-hidden</code> attribute set to <code>"true"</code>.</p>
<h2>See</h2>
<ul>
  <li> <a href="https://www.w3.org/WAI/WCAG21/quickref/?versions=2.0#qr-content-structure-separation-programmatic">WCAG2, 1.3.1</a>&nbsp;-&nbsp;Info
  and Relationships </li>
  <li> <a href="https://www.w3.org/TR/WCAG20-TECHS/H39">WCAG2,&nbsp;H39</a> - Using caption elements to associate data table captions with data tables
  </li>
</ul>