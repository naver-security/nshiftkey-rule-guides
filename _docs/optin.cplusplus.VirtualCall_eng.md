---
title: Use VirtualCall in constructor and destructor
category: ""
order: 0
---

## 1. Vulnerability Description
* Unintentional results can occur because the virtual function does not behave as intended in constructor and destructor.


## 2. Vulnerability Countermeasure
* Do not use VirtualCall in constructor and destructor


## 3. Sample Code
* Vulnerable Code
  * For the code below, there are base and derived classes. At that time, when you create a derived class instance, the base constructor is called before the derived constructor is called.
  * However, the derived class variables are not initialized because the derived constructor has not been called yet.
  * If you call a virtual function in the base constructor, and the virtual function accesses a member of a derived class, error may occur.

```c++
class Transaction
{ // base class for all
  public: // transactions
    Transaction();
    virtual void logTransaction() const = 0;  // make type-dependent
    // log entry
    ...
};

Transaction::Transaction()  // implementation of
{ // base class constructor
    logTransaction(); // as final action, log this
}       
// transaction

class BuyTransaction: public Transaction
{ // derived class
  public:
     virtual void logTransaction() const; // how to log trans-
     ...
};

class SellTransaction: public Transaction
{ // derived class
  public:
    virtual void logTransaction() const; // how to log trans-
    ...
};
```

* Safe Code
  * In the case of the code below, logTransaction is converted into a non-virtual function of the Transaction class.
  
```c++
class Transaction {
public:
    explicit Transaction(const std::string& logInfo);
    void logTransaction(const std::string& logInfo) const;

    ...
};

Transaction::Transaction(const std::string& logInfo)
{
    ...
    logTransaction(logInfo);
}

class BuyTransaction: public Transaction {
public:
    BuyTransaction(parameters) // Call Transaction(createLogString( parameters)) in constructor
    { ... }
    ...

private:
    static std::string createLogString( parameters);
};
```