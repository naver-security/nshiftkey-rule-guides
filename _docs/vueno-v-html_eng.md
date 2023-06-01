---
title: If you use v-html, then there is a possibility of an XSS vulnerability.
category: ""
order: 0
---

## 1. Vulnerability Description
* If you use v-html to dynamically render arbitrary HTML on a website, then there is a possibility of an XSS vulnerability.

## 2. How to check vulnerability
* Make sure If you are using v-html.

## 3.  Vulnerability Countermeasure
* Avoid using v-html if it's possible.
* Make sure to use only trusted content, and if it is inevitable, you must verify the input value.

## 4. Sample Code
* Vulnerable Code
   * For HTML interpolation, if you declare a v-html directive in HTML and assign an attribute to the directive in Vue, it can lead to XSS.

```html
<div id="app" class="container">
   Welcome :
  <span v-html="attack">
   </span>
</div>
```

```js
// extend and register in one step
Vue.component('my-component', {
   //Props camelCase in JS
   props: {
    compLabel: {default:  'Default Label'}
  },
   template: '#textComponent',
   data: function() {
     return { }
   }
})

new Vue({
   el: '#app',
   data: {
      attack: '<a onmouseover=alert(document.cookie)>click me!</a>',
   }
});
```

