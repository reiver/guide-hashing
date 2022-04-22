# MD5 ([Hashing Guide](../../README.md))

by [Charles Iliya Krempeaux](http://changelog.ca/)

---

**MD5** (which is short for **Message-Digest Algorithm 5**) is a **cryptographic hash function** that was popular in the mid-1990s to mid-2000s.

**MD5** is important from a historical point-of-view, as there are a lot of **digests** from the **MD5** cryptographic hash function out-in-the-wild — so you may have to deal with them if you are working with old data, or old systems —

⚠️ But the **MD5** cryptographic hash function is considered **‘broken’** and should **NOT** be used for new systems.

Nevertheless, understanding & using the **MD5** cryptographic hash function will help us understand **hashing** in general, so let's play around with it.

## import "crypto/md5"

The [Go programming language](http://golang.org/) has a built-in support for **MD5**, with its ["crypto/md5"](https://pkg.go.dev/crypto/md5) package.

Let's look at a very simple example of using the [Go programming language](http://golang.org/)'s implementation of **MD5** —

```golang
package main

import (
	"crypto/md5"
	"fmt"
)

func main() {

	// This is our raw data, that we will run through the cryptographic hash function.
	// Feel free to change this, and see what the digest changes to.
	const data string = "Hello world!"
	
	// The ‘md5.Sum()’ cryptographic hash function accepts a ‘[]byte’ as input, rather than a ‘ string’,
	// so we need to convert our ‘string’ stored in ‘data’ into a ‘[]byte’.
	var p []byte = []byte(data)
	
	// Apply the MD5 cryptographic hash function to the data, and get the resulting digest from applying the cryptographic hash function to the data.
	digest := md5.Sum(p)
	
	// Output the digest that was returned from the cryptographic hash function, in hexadecimal format.
	fmt.Printf("digest (in hexadecimal): %x", digest)
}

```

The most important part of this code is:
```golang
digest := md5.Sum(p)
```

[md5.Sum()](https://pkg.go.dev/crypto/md5#Sum) is the [Go programming language](http://golang.org/)'s implementation of the MD5 hash function.

It is the simplest way of applying the **MD5** cryptographic hash function, but not necessarily the _best_ way in some instances.

## Assignment №1

Write a program in the [Go programming language](http://golang.org/) using the ["crypto/md5"](https://pkg.go.dev/crypto/md5)'s [md5.Sum()](https://pkg.go.dev/crypto/md5#Sum) function that —

* accepts the data (it will run through the cryptographic hash function) from `os.Stdin`, and
* output the resulting **digest** in 4 different formats:
  * hexadecimal,
  * base32,
  * base64, and
  * base64url.

Hints:
* [import "fmt"](https://pkg.go.dev/fmt)
* [import "base32"](https://pkg.go.dev/encoding/base32)
* [import "base64"](https://pkg.go.dev/encoding/base64)

## Big Data

In our previous example, the data we applied the **cryptographic hash function** to was relatively small.

But what if the data we want to apply the **cryptographic hash function** to is relatively big‽

What if, in a practical sense, we cannot (or _should not_) put all the data into a `string` or `[]byte`; what do we do then‽

That is where ["crypto/md5"](https://pkg.go.dev/crypto/md5)'s [md5.New()](https://pkg.go.dev/crypto/md5#New) comes into play —

```golang
package main

import (
	"crypto/md5"
	"fmt"
	"io"
)

func main() {

	hasher := md5.New()
	
	// This shows that the data that is being run through a cryptographic hash function
	// can be given to the cryptographic hash function in chunks.
	io.WriteString(hasher, "Hello")
	io.WriteString(hasher, " ")
	hasher.Write([]byte{'w','o','r','l','d'})
	hasher.Write([]byte{'!'})
	
	// Get the resulting digest from applying the cryptographic hash function to the data.
	digest := hasher.Sum(nil)
	
	// Output the digest that was returned from the cryptographic hash function, in hexadecimal format.
	fmt.Printf("digest (in hexadecimal): %x", digest)
}
```

## Assignment №2

---

[⏮](../..//README.md) [⏭️](../sha-1/README.md)
