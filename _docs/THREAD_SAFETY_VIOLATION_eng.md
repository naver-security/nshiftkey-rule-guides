---
title: Thread-safety violation
category: ""
order: 0
---

## 1. Vulnerability Description
* If the same member field is accessed simultaneously, data race can occur.


## 2. Vulnerability Countermeasure
* Access member fields using synchronized keywords, atomic objects, and volatile keywords
* Access from the same thread using @MainThread or @ThreadConfined를

## 3. Sample Code
* Vulnerable Code
  * Unexpected results may occur if multiple threads use the setMemory method in the following calculator classes :

```java
...
public class Calculator {
	private int memory;
	
	public int getMemory(){
		return memory;
	}
	
	public void setMemory(int memory){
		this.memory = memory;
		try{
			Thread.sleep(2000);
		}catch(InterruptedException e){}
		
		System.out.println(Thread.currentThread().getName() + "": "" + this.memory);
	}
}
...
```

* Safe Code
  * Add a synchronized keyword so that no other thread can execute when setting memory

```java
...
public class Calculator {
	private int memory;
	
	public int getMemory(){
		return memory;
	}
	
	public synchronized void setMemory(int memory){
		this.memory = memory;
		try{
			Thread.sleep(2000);
		}catch(InterruptedException e){}
		
		System.out.println(Thread.currentThread().getName() + "": "" + this.memory);
	}
}
...
```
