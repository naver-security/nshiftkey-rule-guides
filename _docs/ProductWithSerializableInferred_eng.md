---
title: Product With Serializable
category: ""
order: 0
---

## 1. Vulnerability Description
* When creating a list, if variables of an unrelated type are entered, type inference may occur as Product with Serializable.


## 2. Vulnerability Countermeasure
* Use by defining extends Product with Serializable in the type of list.

## 3. Sample Code
* Vulnerable Code

```SCALA
scala> trait Animal
defined trait Animal

scala> trait FurryAnimal extends Animal
defined trait FurryAnimal

scala> case class Dog(name:String) extends Animal
defined class Dog

scala> case class Cat(name:String) extends Animal
defined class Cat

scala> val x = Array(Dog("Fido"),Cat("Felix"))
x: Array[Product with Serializable with Animal] = Array(Dog(Fido), Cat(Felix))
```

* Safe Code

```SCALA
scala> trait Animal extends Product with Serializable
defined trait Animal

scala> case class Dog(name: String) extends Animal
defined class Dog

scala> case class Cat(name: String) extends Animal
defined class Cat

scala> Array(Dog("d"), Cat("c"))
res0: Array[Animal] = Array(Dog(d), Cat(c))
```
