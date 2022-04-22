# MD5 & Big Data ([Hashing Guide](../../../../../../README.md))

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
	
	// Output the digest that was returned from the cryptographic hash function, as a sequence of bytes in decimal format.
	fmt.Printf("digest (sequece of bytes in decimal)", digest)
	
	// Output the digest that was returned from the cryptographic hash function, in hexadecimal format.
	fmt.Printf("digest (in hexadecimal): %x", digest)
}
```

Here is the key part:
```golang
	io.WriteString(hasher, "Hello")
	io.WriteString(hasher, " ")
	hasher.Write([]byte{'w','o','r','l','d'})
	hasher.Write([]byte{'!'})```
```

Note that gave the data to the **hash function** in chunks:
* `"Hello"`
* `" "`
* `"world"`
* "!"

In this example, our data is small; but we can keep on giving it more and more and more chunks when the data is big.

For example:
```golang
for {

	// ...

	n, err := hasher.Write(p)

	// ...

}
```
