---
title: Mismatch between Alloc and Dealloc method
category: ""
order: 0
---

## 1. Vulnerability Description
* Crash may occur if memory allocation methods and deallocation methods are not matched.


## 2. Vulnerability Countermeasure
* Use matching functions such as Malloc/free, new/delete, new[]/delete[] when alloc/dealloc.
* See the table below for more information on the matching functions

Allocator | Deallocator
-- | --
new | delete
malloc() | free()
realloc() | free()
LocalAlloc() | LocalFree()
LocalReAlloc() | LocalFree()
GlobalAlloc() | GlobalFree()
GlobalReAlloc() | GlobalFree()
VirtualAlloc() | VirtualFree()
VirtualAllocEx() | VirtualFreeEx()
VirtualAllocExNuma() | VirtualFreeEx()
AllocateUserPhysicalPages() | FreeUserPhysicalPages()
AllocateUserPhysicalPagesNuma() | FreeUserPhysicalPages()
HeapAlloc() | HeapFree()
HeapReAlloc() | HeapFree()


## 3. Sample Code
* Vulnerable Code
```c
LPTSTR buf;
DWORD n = FormatMessage(FORMAT_MESSAGE_ALLOCATE_BUFFER |
                        FORMAT_MESSAGE_FROM_SYSTEM |
                        FORMAT_MESSAGE_IGNORE_INSERTS, 0, GetLastError(),
                        LANG_USER_DEFAULT, (LPTSTR)&buf, 1024, 0);
if (n != 0) {
  /* Format and display the error to the user */
 
  GlobalFree(buf);
}
```

* Safe Code
```c
LPTSTR buf;
DWORD n = FormatMessage(FORMAT_MESSAGE_ALLOCATE_BUFFER |
                        FORMAT_MESSAGE_FROM_SYSTEM |
                        FORMAT_MESSAGE_IGNORE_INSERTS, 0, GetLastError(),
                        LANG_USER_DEFAULT, (LPTSTR)&buf, 1024, 0);
if (n != 0) {
  /* Format and display the error to the user */
 
  LocalFree(buf);
}
```