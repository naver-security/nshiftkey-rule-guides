---
title: Resource leak
category: ""
order: 0
---


## 1. Vulnerability Description
Access to external resources using methods in Java (in/out stream, reader, writer, sockets, http connections, cursors, json parameters, etc.) should be closed after use, otherwise resource leakage may occur.


## 2. Vulnerability Countermeasure
All finished objects must be closed. Or you can use try-with-resource to make auto close.

## 3. Example Codd
* Vulnerable code

```c++
public static void main(String[] args) {
    FileInputStream fis = null;
    try{
         fis = new FileInputStream("""");
    }catch(IOException e){
        
    }finally {
        // Closing may result in exceptions
        fis.close();
    }
}
```


* Safe code

```c++
public static void main(String[] args) {
    // With try-with-resource enabled, automatically close after try/catch.
    try(FileInputStream fis = new FileInputStream("""")){
         
    }catch(IOException e){

    }
}

```
