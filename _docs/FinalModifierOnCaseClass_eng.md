---
title: Missing final modifier in case class
category: ""
order: 0
---

## 1. Vulnerability Description
* If you extend a case class, It cause unintended operation.

## 2. Vulnerability Countermeasure
* Do not extend the case class.

## 3. Sample Code
* Vulnerable Code

```SCALA
// Definition
case class Foo(i: Int)
class Bar(i: Int, s: String) extends Foo(i)


// example
new Bar(1, "foo") == new Bar(1, "bar")
// res0: Boolean = true

Map(
new Bar(1, "foo") -> "foo",
new Bar(1, "bar") -> "bar"
)
// res1: Map[Bar, String] = Map(Foo(1) -> "bar")

new Bar(1, "baz")
// res2: Bar = Foo(1)
```

