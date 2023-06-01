---
title: Generate predictable random values
category: ""
order: 0
---

## 1. Vulnerability Description
* When creating predictable random values and using them as security elements such as session IDs and tokens, an attacker can predict random values and attack the system. 
* Since rand() has a constant base number, it can reproduce a random number that returns a value corresponding to the seed value and can generate predictable random values.

## 2. How to check vulnerability
Check to import and use math/rand with the random package.

## 3. Vulnerability Countermeasure
The crypto/rand package implements and uses a cryptographically secure random number generator.
The crypto/rand package can be used to prevent the vulnerability.

## 4. Sample Code
* Vulnerable Code

```go
package main

import (
    "fmt"
    "time"
    "math/rand"
)

func main() {
    rand.Seed(time.Now().UnixNano())
    fmt.Println(rand.Intn(100))
}
```


* Safe Code

```go
package main

import (
    ""crypto/rand""
    ""fmt""
    ""math/big""
)

func main() {
    n, err := rand.Int(rand.Reader, big.NewInt(100))
    if err != nil {
        panic(err)
    }
    fmt.Println(n)
}
```
