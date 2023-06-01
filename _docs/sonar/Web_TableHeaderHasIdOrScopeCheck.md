---
title: ""
category: ""
order: 0
---

<h1>"&lt;th&gt;" tags should have "id" or "scope" attributes</h1>
<small>Web:TableHeaderHasIdOrScopeCheck</small>
<br>
<p>Associating <code>&lt;table&gt;</code> headers, i.e. <code>&lt;th&gt;</code> elements, with their <code>&lt;td&gt;</code> cells enables screen
readers to announce the header prior to the data. This considerably increases the accessibility of tables to visually impaired users.</p>
<p>There are two ways of doing it:</p>
<ul>
  <li> Adding a <code>scope</code> attribute to <code>&lt;th&gt;</code> headers. </li>
  <li> Adding an <code>id</code> attribute to <code>&lt;th&gt;</code> headers and a <code>headers</code> attribute to every <code>&lt;td&gt;</code>
  element. </li>
</ul>
<p>It is recommended to add <code>scope</code> attributes to <code>&lt;th&gt;</code> headers whenever possible. Use <code>&lt;th id="..."&gt;</code>
and <code>&lt;td headers="..."&gt;</code> only when <code>&lt;th scope="..."&gt;</code> is not capable of associating cells to their headers. This
happens for very complex tables which have headers splitting the data in multiple subtables. See&nbsp;<a
href="https://www.w3.org/WAI/tutorials/tables/tips/">W3C WAI&nbsp;Web Accessibility Tutorials</a>&nbsp;for more information.</p>
<p>Note that complex tables can often be split into multiple smaller tables, which improves the user experience.</p>
<p>This rule raises an issue when a <code>&lt;th&gt;</code> element has neither <code>id</code> nor <code>scope</code> attributes set.</p>
<h2>Noncompliant Code Example</h2>
<pre>
&lt;table border="1"&gt;
  &lt;caption&gt;Contact Information&lt;/caption&gt;
  &lt;tr&gt;
    &lt;td&gt;&lt;/td&gt;
    &lt;th&gt;Name&lt;/th&gt;                                          &lt;!-- Non-Compliant --&gt;
    &lt;th&gt;Phone#&lt;/th&gt;                                        &lt;!-- Non-Compliant --&gt;
    &lt;th&gt;City&lt;/th&gt;                                          &lt;!-- Non-Compliant --&gt;
  &lt;/tr&gt;
  &lt;tr&gt;
    &lt;td&gt;1.&lt;/td&gt;
    &lt;th&gt;Joel Garner&lt;/th&gt;                                   &lt;!-- Non-Compliant --&gt;
    &lt;td&gt;412-212-5421&lt;/td&gt;
    &lt;td&gt;Pittsburgh&lt;/td&gt;
  &lt;/tr&gt;
  &lt;tr&gt;
    &lt;td&gt;2.&lt;/td&gt;
    &lt;th&gt;Clive Lloyd&lt;/th&gt;                                   &lt;!-- Non-Compliant --&gt;
    &lt;td&gt;410-306-1420&lt;/td&gt;
    &lt;td&gt;Baltimore&lt;/td&gt;
  &lt;/tr&gt;
&lt;/table&gt;
</pre>
<h2>Compliant Solution</h2>
<pre>
&lt;table border="1"&gt;
  &lt;caption&gt;Contact Information&lt;/caption&gt;
  &lt;tr&gt;
    &lt;td&gt;&lt;/td&gt;
    &lt;th scope="col"&gt;Name&lt;/th&gt;                              &lt;!-- Compliant --&gt;
    &lt;th scope="col"&gt;Phone#&lt;/th&gt;                            &lt;!-- Compliant --&gt;
    &lt;th scope="col"&gt;City&lt;/th&gt;                              &lt;!-- Compliant --&gt;
  &lt;/tr&gt;
  &lt;tr&gt;
    &lt;td&gt;1.&lt;/td&gt;
    &lt;th scope="row"&gt;Joel Garner&lt;/th&gt;                       &lt;!-- Compliant --&gt;
    &lt;td&gt;412-212-5421&lt;/td&gt;
    &lt;td&gt;Pittsburgh&lt;/td&gt;
  &lt;/tr&gt;
  &lt;tr&gt;
    &lt;td&gt;2.&lt;/td&gt;
    &lt;th scope="row"&gt;Clive Lloyd&lt;/th&gt;                       &lt;!-- Compliant --&gt;
    &lt;td&gt;410-306-1420&lt;/td&gt;
    &lt;td&gt;Baltimore&lt;/td&gt;
  &lt;/tr&gt;
&lt;/table&gt;
</pre>
<p>or:</p>
<pre>
&lt;table border="1"&gt;
  &lt;caption&gt;Contact Information&lt;/caption&gt;
  &lt;tr&gt;
    &lt;td&gt;&lt;/td&gt;
    &lt;th id="name"&gt;Name&lt;/th&gt;                                &lt;!-- Compliant --&gt;
    &lt;th id="phone"&gt;Phone#&lt;/th&gt;                             &lt;!-- Compliant --&gt;
    &lt;th id="city"&gt;City&lt;/th&gt;                                &lt;!-- Compliant --&gt;
  &lt;/tr&gt;
  &lt;tr&gt;
    &lt;td&gt;1.&lt;/td&gt;
    &lt;th id="person1" headers="name"&gt;Joel Garner&lt;/th&gt;       &lt;!-- Compliant --&gt;
    &lt;td headers="phone person1"&gt;412-212-5421&lt;/td&gt;
    &lt;td headers="city person1"&gt;Pittsburgh&lt;/td&gt;
  &lt;/tr&gt;
  &lt;tr&gt;
    &lt;td&gt;2.&lt;/td&gt;
    &lt;th id="person2" headers="name"&gt;Clive Lloyd&lt;/th&gt;       &lt;!-- Compliant --&gt;
    &lt;td headers="phone person2"&gt;410-306-1420&lt;/td&gt;
    &lt;td headers="city person2"&gt;Baltimore&lt;/td&gt;
  &lt;/tr&gt;
&lt;/table&gt;
</pre>
<h2>Exceptions</h2>
<p>This rule is not applied in case of simple tables.</p>
<p>Tables are considered as such when the headers are either all in the first row, or all in the first column. The two conditions must not apply
together.</p>
<p>Simple table example:</p>
<pre>
&lt;table border="1"&gt;
    &lt;caption&gt;Simple Table 1&lt;/caption&gt;
    &lt;tr&gt;
        &lt;th&gt;Name&lt;/th&gt;
        &lt;th&gt;Surname&lt;/th&gt;
    &lt;/tr&gt;
    &lt;tr&gt;
        &lt;td&gt;John&lt;/td&gt;
        &lt;td&gt;Doe&lt;/td&gt;
    &lt;/tr&gt;
&lt;/table&gt;
&lt;table border="1"&gt;
    &lt;caption&gt;Simple Table 2&lt;/caption&gt;
    &lt;tr&gt;
        &lt;th&gt;Name&lt;/th&gt;
        &lt;td&gt;John&lt;/td&gt;
    &lt;/tr&gt;
    &lt;tr&gt;
        &lt;th&gt;Surname&lt;/th&gt;
        &lt;td&gt;Doe&lt;/td&gt;
    &lt;/tr&gt;
&lt;/table&gt;
</pre>
<h2>See</h2>
<ul>
  <li> <a href="https://www.w3.org/WAI/WCAG21/quickref/?versions=2.0#qr-content-structure-separation-programmatic">WCAG2, 1.3.1</a>&nbsp;-&nbsp;Info
  and Relationships </li>
  <li> <a href="https://www.w3.org/TR/WCAG20-TECHS/html.html#H43">WCAG2, H43</a> - Using id and headers attributes to associate data cells with header
  cells in data tables </li>
</ul>