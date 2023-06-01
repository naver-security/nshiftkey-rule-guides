---
title: STRICT mode violation
category: ""
order: 0
---

## 1. Vulnerability Description
* It is detected when an act violates the STRICT mode.
* If the main thread performs tasks such as disk I/O or network access, the app's responsiveness may become slow and an "Application Not Responding" error may occur.

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
