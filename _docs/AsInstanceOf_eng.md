---
title: Incomplete type inference
category: ""
order: 0
---

## 1. Vulnerability Description
* Using AsInstanceOf, IsInstanceOf to deduce types can lead to incorrect type reasoning and unexpected errors. In particular, since Scala has a type erase at the time of compilation, the developer must know the type of variable explicitly.

## 2. Vulnerability Countermeasure
* Use pattern matching for Type to explicitly enable type-specific processing.

## 3. Sample Code
* Pattern matching example

```JAVA
abstract class Device
case class Phone(model: String) extends Device {
  def screenOff = "Turning screen off"
}
case class Computer(model: String) extends Device {
  def screenSaverOn = "Turning screen saver on..."
}

def goIdle(device: Device) = device match {
  case p: Phone => p.screenOff
  case c: Computer => c.screenSaverOn
}
```

