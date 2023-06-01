---
title: Suspicious memory leak in std::basic_string
category: ""
order: 0
---

## 1. Vulnerability Description
* Crash can occur when writing memory using functions such as memset(), memcpy() for class variables with reference.


## 2. Vulnerability Countermeasure
* When using variables in C++ style, it is important to utilize variable assignment and initialization methods of C++ style. When initializing variables in a class object, make sure to do so individually for each variable.

* When you use variables of C++ styles, you also must use variable assignment, initialized methods of C++ styles. When initializing variables in class object, make sure to do so individually for each variable.


## 3. Sample Code
* Vulnerable Code

```c++
ConfigurationImpl::ConfigurationImpl() {
private:
	float total;
	int score1;
	int score2;
public:
	float Add(float num1, float num2) {
		return num1 + num2;
	}
	float Div(float num1, float num2) {
		return num1/num2;
	}
}

int main(void) {
	ConfigurationImpl conf;    
        memset(conf, 0, sizeof(ConfigurationImpl));  // Initialize all members to zero.
	...
}
```

* Safe Code

```c++
ConfigurationImpl::ConfigurationImpl() {
private:
	float total;
	int score1;
	int score2;
public:
	void Init() {
		total = 0;
		score1 = 0;
	        score2 = 0;
	}
	float Add(float num1, float num2) {
		return num1 + num2;
	}
	float Div(float num1, float num2) {
		return num1/num2;
	}
}

int main(void) {
	ConfigurationImpl conf;
        conf.Init();
	...
}
```
