---
title: Zip Slip
category: ""
order: 0
---

## 1. Vulnerability Description
The vulnerability is exploited using a specially crafted archive that holds directory traversal filenames (e.g. ../../evil.sh). The Zip Slip vulnerability can affect numerous archive formats, including tar, jar, war, cpio, apk, rar and 7z.
The premise of the directory traversal vulnerability is that an attacker can gain access to parts of the file system outside of the target folder in which they should reside. The attacker can then overwrite executable files and either invoke them remotely or wait for the system or user to call them, thus achieving remote command execution on the victim’s machine.

## 2. Vulnerability Countermeasure
Before reading the unzipped file, make sure the file has the correct path.
If you use tar, jar, war, cpio, apk, rar and 7z, be sure to use a safe version of the compression library.
 

## 3. Sample Code
* Vulnerable golang Code

```go
func (rarFormat) Read(input io.Reader, dest string) {
     rr := rardecode.NewReader(input, """")
     for {
         header := rr.Next()
         writeNewFile(filepath.Join(dest, header.Name), rr, header.Mode())
     }
}
```


* Safe golang Code

```go
func sanitizeExtractPath(filePath string, destination string) error {
    destpath := filepath.Join(destination, filePath)
    if !strings.HasPrefix(destpath, filepath.Clean(destination) + string(os.PathSeparator)) {
        return fmt.Errorf(""%s: illegal file path"", filePath)
    }
    return nil
}
```
