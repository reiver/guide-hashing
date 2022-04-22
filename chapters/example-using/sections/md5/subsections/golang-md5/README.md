# import "crypto/md5" ([Hashing Guide](../../README.md))

by [Charles Iliya Krempeaux](http://changelog.ca/)

---

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

	// Output the digest that was returned from the cryptographic hash function, as a sequence of bytes in decimal format.
	fmt.Printf("digest (sequece of bytes in decimal)", digest)

	// Output the digest that was returned from the cryptographic hash function, in hexadecimal format.
	fmt.Printf("digest (hexadecimal): %x \n", digest)
}

```

The most important part of this code is:
```golang
digest := md5.Sum(p)
```

[md5.Sum()](https://pkg.go.dev/crypto/md5#Sum) is the [Go programming language](http://golang.org/)'s implementation of the MD5 hash function.

It is the simplest way of applying the **MD5** cryptographic hash function, but not necessarily the _best_ way in some instances (as we will explore later on).

---

[⏮](../../README.md) [⬆️](../../README.md) [⏭️](../assignment-1/README.md)
