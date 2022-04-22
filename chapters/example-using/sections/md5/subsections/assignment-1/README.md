# MD5 Assignment №1 ([Hashing Guide](../../../../../../README.md))

by [Charles Iliya Krempeaux](http://changelog.ca/)

---

Write a program in the [Go programming language](http://golang.org/) using the ["crypto/md5"](https://pkg.go.dev/crypto/md5)'s [md5.Sum()](https://pkg.go.dev/crypto/md5#Sum) function that —

* accepts the data (it will run through the cryptographic hash function) from `os.Stdin`, and
* output the resulting **digest** in 5 different formats:
  * sequece of bytes in decimal
  * hexadecimal,
  * base32,
  * base64, and
  * base64url.

So, for example, if the input to your program is the equivalent of:
```golang
"Hello world! [1]"
```
I.e.,:
```golang
[]byte{'H','e','l','l','o',' ','w','o','r','l','d','!',' ','['.'1',']'}
```

Then your program should output:
```
digest (sequece of bytes in decimal): [29 19 210 215 234 102 26 37 2 25 192 193 249 95 190 99] 
digest (hexadecimal): 1d13d2d7ea661a250219c0c1f95fbe63 
digest (base32):      DUJ5FV7KMYNCKAQZYDA7SX56MM====== 
digest (base64):      HRPS1+pmGiUCGcDB+V++Yw==
digest (base64url):   HRPS1-pmGiUCGcDB-V--Yw
```

Hints:
* [import "base32"](https://pkg.go.dev/encoding/base32)
* [import "base64"](https://pkg.go.dev/encoding/base64)
* [import "fmt"](https://pkg.go.dev/fmt)

---

[⏮](../golang-md5/README.md) [⬆️](../../README.md) [⏭️](../big-data/README.md)
