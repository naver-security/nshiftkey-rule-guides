---
title: case / match type comparison impossible
category: ""
order: 0
---

## 1. Vulnerability Description
* If the variable to be compared and the case class object in the match statement cannot be compared with each other, an unintended error may occur.

## 2. Vulnerability Countermeasure
Make sure that the comparison target is correct.

## 3. Sample Code
* Vulnerable Code

```SCALA
trait Machine
case class Terminator(name:String) extends Machine
class Test {
    def b : Any = 4
    b match {
    case Terminator =>
    case _ =>
    }
}
```
