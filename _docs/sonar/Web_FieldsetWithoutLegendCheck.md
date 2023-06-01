---
title: ""
category: ""
order: 0
---

<h1>"&lt;fieldset&gt;" tags should contain a "&lt;legend&gt;"</h1>
<small>Web:FieldsetWithoutLegendCheck</small>
<br>
<p>For users of assistive technology such as screen readers, it may be challenging to know what is expected in each form’s input. The input’s label
alone might not be sufficient: 'street' could be part of a billing or a shipping address for instance.</p>
<p>Fieldset legends are read out loud by screen readers before the label each time the focus is set on an input. For example, a legend 'Billing
address' with a label 'Street' will read 'Billing address street'. Legends should be short, and 'Your' should not be repeated in both the legend and
the label, as it would result in 'Your address Your City' being read.</p>
<h2>Noncompliant Code Example</h2>
<pre>
&lt;fieldset&gt;                                 &lt;!-- Noncompliant --&gt;
  Street: &lt;input type="text"&gt;&lt;br /&gt;
  Town: &lt;input type="text"&gt;&lt;br /&gt;
  Country: &lt;input type="text"&gt;&lt;br /&gt;
&lt;/fieldset&gt;
</pre>
<h2>Compliant Solution</h2>
<pre>
&lt;fieldset&gt;
  &lt;legend&gt;Billing address&lt;/legend&gt;
  Street: &lt;input type="text"&gt;&lt;br /&gt;
  Town: &lt;input type="text"&gt;&lt;br /&gt;
  Country: &lt;input type="text"&gt;&lt;br /&gt;
&lt;/fieldset&gt;
</pre>