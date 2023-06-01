---
title: Resource shortage due to main thread overload
category: ""
order: 0
---

## 1. Vulnerability Description
* If you do something that occupies the CPU for a long time on the UI thread, you lose control of your app with an "Application Not Responding" error.

## 2. Vulnerability Countermeasure
* In situations where the app is potentially working for a long time, instead of working on UI threads, you must create worker threads and perform most of the tasks on worker threads.

## 3. Sample Code
* Vulnerable Code
   * UI thread consumes a lot of time when data is too large

```java
    @Override
    public void onClick(View view) {
        // This task runs on the main thread.
        BubbleSort.sort(data);
    }
```


* Safe Code
   * Allow AsyncTask to handle long-lasting tasks by worker threads
   
```java
    @Override
    public void onClick(View view) {
       // The long-running operation is run on a worker thread
       new AsyncTask<Integer[], Integer, Long>() {
           @Override
           protected Long doInBackground(Integer[]... params) {
               BubbleSort.sort(params[0]);
           }
       }.execute(data);
    }
```
