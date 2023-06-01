---
title: ""
category: ""
order: 0
---

<h1>Image, area and button with image tags should have an "alt" attribute</h1>
<small>Web:ImgWithoutAltCheck</small>
<br>
<p>The <code>alt</code> attribute provides a textual alternative to an image.</p>
<p>It is used whenever the actual image cannot be rendered.</p>
<p>Common reasons for that include:</p>
<ul>
  <li> The image can no longer be found </li>
  <li> Visually impaired users using a screen reader software </li>
  <li> Images loading is disabled, to reduce data consumption on mobile phones </li>
</ul>
<p>It is also very important to not set an <code>alt</code> attribute to a non-informative value. For example <code>&lt;img ... alt="logo"&gt;</code>
is useless as it doesn’t give any information to the user. In this case, as for any other decorative image, it is better to use a CSS background image
instead of an <code>&lt;img&gt;</code> tag. If using CSS background-image is not possible, an empty <code>alt=""</code> is tolerated. See Exceptions
bellow.</p>
<p>This rule raises an issue when</p>
<ul>
  <li> an <code>&lt;input type="image"&gt;</code> tag or an <code>&lt;area&gt;</code> tag have no <code>alt</code> attribute or their
  <code>alt</code>&nbsp;attribute has an empty string value. </li>
  <li> an <code>&lt;img&gt;</code> tag has no <code>alt</code> attribute. </li>
</ul>
<h2>Noncompliant Code Example</h2>
<pre>
&lt;img src="foo.png" /&gt; &lt;!-- Noncompliant --&gt;
&lt;input type="image" src="bar.png" /&gt; &lt;!-- Noncompliant --&gt;
&lt;input type="image" src="bar.png" alt="" /&gt; &lt;!-- Noncompliant --&gt;

&lt;img src="house.gif" usemap="#map1"
    alt="rooms of the house." /&gt;
&lt;map id="map1" name="map1"&gt;
  &lt;area shape="rect" coords="0,0,42,42"
    href="bedroom.html"/&gt; &lt;!-- Noncompliant --&gt;
  &lt;area shape="rect" coords="0,0,21,21"
    href="lounge.html" alt=""/&gt; &lt;!-- Noncompliant --&gt;
&lt;/map&gt;
</pre>
<h2>Compliant Solution</h2>
<pre>
&lt;img src="foo.png" alt="Some textual description of foo.png" /&gt;
&lt;input type="image" src="bar.png" alt="Textual description of bar.png" /&gt;

&lt;img src="house.gif" usemap="#map1"
    alt="rooms of the house." /&gt;
&lt;map id="map1" name="map1"&gt;
  &lt;area shape="rect" coords="0,0,42,42"
    href="bedroom.html" alt="Bedroom" /&gt;
  &lt;area shape="rect" coords="0,0,21,21"
    href="lounge.html" alt="Lounge"/&gt;
&lt;/map&gt;
</pre>
<h2>Exceptions</h2>
<p><code>&lt;img&gt;</code> tags with empty string&nbsp;<code>alt=""</code> attributes won’t raise any issue. However this technic should be used in
two cases only:</p>
<p>When the image is decorative and it is not possible to use a CSS background image. For example, when the decorative <code>&lt;img&gt;</code> is
generated via javascript with a source image coming from a database, it is better to use an <code>&lt;img alt=""&gt;</code> tag rather than generate
CSS code.</p>
<pre>
&lt;li *ngFor="let image of images"&gt;
    &lt;img [src]="image" alt=""&gt;
&lt;/li&gt;
</pre>
<p>When the image is not decorative but it’s <code>alt</code> text would repeat a nearby text. For example, images contained in links should not
duplicate the link’s text in their <code>alt</code> attribute, as it would make the screen reader repeat the text twice.</p>
<pre>
&lt;a href="flowers.html"&gt;
    &lt;img src="tulip.gif" alt="" /&gt;
    A blooming tulip
&lt;/a&gt;
</pre>
<p>In all other cases you should use CSS background images.</p>
<p>See&nbsp;<a href="https://www.w3.org/WAI/tutorials/images/decision-tree/">W3C WAI&nbsp;Web Accessibility Tutorials</a>&nbsp;for more
information.</p>
<h2>See</h2>
<ul>
  <li> <a href="https://www.w3.org/TR/WCAG20-TECHS/H24.html">WCAG2, H24</a> - Providing text alternatives for the area elements of image maps </li>
  <li> <a href="https://www.w3.org/TR/WCAG20-TECHS/H36.html">WCAG2, H36</a> - Using alt attributes on images used as submit buttons </li>
  <li> <a href="https://www.w3.org/TR/WCAG20-TECHS/H37.html">WCAG2, H37</a> - Using alt attributes on img elements </li>
  <li> <a href="https://www.w3.org/TR/WCAG20-TECHS/H67.html">WCAG2, H67</a> - Using null alt text and no title attribute on img elements for images
  that AT should ignore </li>
  <li> <a href="https://www.w3.org/TR/WCAG20-TECHS/H2.html">WCAG2, H2</a> - Combining adjacent image and text links for the same resource </li>
  <li> <a href="https://www.w3.org/WAI/WCAG21/quickref/?versions=2.0#qr-text-equiv-all">WCAG2, 1.1.1</a> - Non-text Content </li>
  <li> <a href="https://www.w3.org/WAI/WCAG21/quickref/?versions=2.0#qr-navigation-mechanisms-refs">WCAG2, 2.4.4</a> - Link Purpose (In Context) </li>
  <li> <a href="https://www.w3.org/WAI/WCAG21/quickref/?versions=2.0#qr-navigation-mechanisms-link">WCAG2, 2.4.9</a> - Link Purpose (Link Only) </li>
</ul>