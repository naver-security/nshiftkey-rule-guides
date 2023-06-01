---
title: ""
category: ""
order: 0
---

<h1>Elements deprecated in HTML5 should not be used</h1>
<small>Web:UnsupportedTagsInHtml5Check</small>
<br>
<p>With the advent of HTML5, many old elements were deprecated. To ensure the best user experience, deprecated elements should not be used. This rule
checks for the following deprecated elements:</p>
<table>
  <colgroup>
    <col style="width: 50%;">
    <col style="width: 50%;">
  </colgroup>
  <thead>
    <tr>
      <th>Element</th>
      <th>Remediation Action</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><p><code>basefont</code>, <code>big</code>, <code>blink</code>, <code>center</code>, <code>font</code>, <code>marquee</code>,
      <code>multicol</code>, <code>nobr</code>, <code>spacer</code>, <code>tt</code></p></td>
      <td><p>use CSS</p></td>
    </tr>
    <tr>
      <td><p><code>acronym</code></p></td>
      <td><p>use <code>abbr</code></p></td>
    </tr>
    <tr>
      <td><p><code>applet</code></p></td>
      <td><p>use <code>embed</code> or <code>object</code></p></td>
    </tr>
    <tr>
      <td><p><code>bgsound</code></p></td>
      <td><p>use <code>audio</code></p></td>
    </tr>
    <tr>
      <td><p><code>frame</code>, <code>frameset</code>, <code>noframes</code></p></td>
      <td><p>restructure the page to remove frames</p></td>
    </tr>
    <tr>
      <td><p><code>isindex</code></p></td>
      <td><p>use form controls</p></td>
    </tr>
    <tr>
      <td><p><code>dir</code></p></td>
      <td><p>use <code>ul</code></p></td>
    </tr>
    <tr>
      <td><p><code>hgroup</code></p></td>
      <td><p>use <code>header</code> or <code>div</code></p></td>
    </tr>
    <tr>
      <td><p><code>listing</code></p></td>
      <td><p>use <code>pre</code> and <code>code</code></p></td>
    </tr>
    <tr>
      <td><p><code>nextid</code></p></td>
      <td><p>use GUIDS</p></td>
    </tr>
    <tr>
      <td><p><code>noembed</code></p></td>
      <td><p>use <code>object</code> instead of <code>embed</code> when fallback is necessary</p></td>
    </tr>
    <tr>
      <td><p><code>plaintext</code></p></td>
      <td><p>use the "text/plain" MIME type</p></td>
    </tr>
    <tr>
      <td><p><code>strike</code></p></td>
      <td><p>use <code>del</code> or <code>s</code></p></td>
    </tr>
    <tr>
      <td><p><code>xmp</code></p></td>
      <td><p>use <code>pre</code> or <code>code</code>, and escape "&lt;" and "&amp;" characters</p></td>
    </tr>
  </tbody>
</table>
<h2>See</h2>
<ul>
  <li> W3C, <a href="https://www.w3.org/TR/html5-diff">Obsolete Features</a> </li>
  <li> WHATWG, <a href="https://html.spec.whatwg.org/multipage/obsolete.html">Obsolete Features</a> </li>
</ul>