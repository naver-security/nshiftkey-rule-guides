---
title: Use closed file pointer
category: ""
order: 0
---

## 1. Vulnerability Description
* If you use the closed file pointer, you can perform an unintended action.

## 2. Vulnerability Countermeasure
* Do not use closed file pointer


## 3. Sample Code
* Vulnerable Code

```c
#include <stdio.h>
int main( )
{
	FILE *pFile = NULL;
	pFile = fopen( "text.txt", "w+t" );
	if( pFile != NULL ) {
		fputs( "test1", pFile );
		fclose( pFile );
	} 
        ...
        fputs( "test2", pFile );
	return 0;
}
```

* Safe Code

```c
#include <stdio.h>
int main( )
{
	FILE *pFile = NULL;
	pFile = fopen( "text.txt", "w+t" );
	if( pFile != NULL ) {
		fputs( "test1", pFile );
		fclose( pFile );
		pFile = NULL;
	} 
        ...
	return 0;
}
```
