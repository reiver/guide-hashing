# MD5 ([Hashing Guide](../../README.md))

by [Charles Iliya Krempeaux](http://changelog.ca/)

---

**MD5** (which is short for **Message-Digest Algorithm 5**) is a **cryptographic hash function** that was popular in the mid-1990s to mid-2000s.

**MD5** is important from a historical point-of-view, as there are a lot of **digests** from the **MD5** cryptographic hash function out-in-the-wild — so you may have to deal with them if you are working with old data, or old systems —

⚠️ But the **MD5** cryptographic hash function is considered **‘broken’** and should **NOT** be used for new systems.

Nevertheless, understanding & using the **MD5** **cryptographic hash function** will help us understand **hashing** in general, so let's play around with it.

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

	// Output the digest that was returned from the cryptographic hash function, as a sequence of bytes in decimal format.
	fmt.Printf("digest (sequece of bytes in decimal)", digest)

	// Output the digest that was returned from the cryptographic hash function, in hexadecimal format.
	fmt.Printf("digest (in hexadecimal): %x \n", digest)
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
* [import "base32"](https://pkg.go.dev/encoding/base32)
* [import "base64"](https://pkg.go.dev/encoding/base64)
* [import "fmt"](https://pkg.go.dev/fmt)


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
	
	// Output the digest that was returned from the cryptographic hash function, as a sequence of bytes in decimal format.
	fmt.Printf("digest (sequece of bytes in decimal)", digest)
	
	// Output the digest that was returned from the cryptographic hash function, in hexadecimal format.
	fmt.Printf("digest (in hexadecimal): %x", digest)
}
```

## Assignment №2

Write a program in the [Go programming language](http://golang.org/) using the ["crypto/md5"](https://pkg.go.dev/crypto/md5)'s [md5.New()](https://pkg.go.dev/crypto/md5#New) function that —

* accepts the data (it will run through the cryptographic hash function) by opening a file specified by `os.Arg[1]`,
* reads in data from the file **256 bytes** at a time, and
* output the resulting **digest** in 5 different formats:
  * sequence of bytes in decimal format,
  * hexadecimal format,
  * base32 format,
  * base64 format, and
  * base64url format.

So, reading in the data **256 bytes** at a time could be done by reading it into a buffer such as:
```golang
var buffer [256]byte

// ...

for // ...

	n1, err := file.Read(buffer[:])

	// ...
	
	n2, err := hasher.Write(buffer[:n1])
```

Hints:
* [import "base32"](https://pkg.go.dev/encoding/base32)
* [import "base64"](https://pkg.go.dev/encoding/base64)
* [import "fmt"](https://pkg.go.dev/fmt)
* [import "os"](https://pkg.go.dev/os)

## Assignment №3

A **URN** (short for **Uniform Resource Name**) is a URL-like technology that is meant to be used to create globally unique identifiers.

Here are some example **URN**s:

* `urn:ietf:rfc:2648` — The IETF's RFC 2648
* `urn:isbn:0897899245` — The ISBN identifying the hardcover book by El-Sayed El-Aswad titled “Religion and Folk Cosmology: Scenarios of the Visible and Invisible in Rural Egypt” 
* `urn:uuid:f81d4fae-7dec-11d0-a765-00a0c91e6bf6` — a UUID as a URN.
* `urn:xmlorg:objects:dtd:xml:docbook:v4.1.2`
* `urn:xmpp:delay` — Used as an XML-namespace for XMPP's delayed-delivery technology.

At one point, **MD5** **digests** were serialized in a **URN** format. For example:

* `urn:md5:86fb269d190d2c85f6e0468ceca42a20`

These **MD5** **URN**s were, for example, used with **magnet URI**s, which were used with some content-addressable systems.

I.e., if the hexadecimal serialization of an **MD5** **digest** digest is:
```
86fb269d190d2c85f6e0468ceca42a20
```

Then its **MD5** **URN** serialization would be:
```
urn:md5:86fb269d190d2c85f6e0468ceca42a20
```

I.e.,:
```
urn:md5:{hexadecimal-of-md5-digest}
```

⚠️ Although note that with digests from other cryptographic hash functions, they may use other serializations besides hexadecimal. For example — **SHA-1** **URN**s use **base32** for serialization (rather than **hexadecimal**).

## Assignment №4

**Magnet URI**s have been used as a way of making some **URN**s easier to work with.

(For example, JavaScript on a web-page would look for **magnet URI**s, and do some magic with a known TCP port range, to make native applications available to the user using the web browser.)

The **MD5** **URN** was one of the **URN** types that were used with **magnet URI**s. For example:
```
magnet:?xt=urn:md5:86fb269d190d2c85f6e0468ceca42a20
```

Your assignment is to write a program that outputs a **magnet URI** with a `xt` set to the **MD5** **URN** for data.

## Assignment №5

**Named Information URI**

## Assignment №6

**Hash URI**

## Assignment №7

The **HTTP** protocol once had a `Content-MD5` header that was intended to be used for **message integrity**.

I.e., basically that the content the HTTP client receives is what the HTTP server actually sent.

And this the content hasn't been changed due to network error, computer error, tampering, etc.

The HTTP **Content-MD5** header looks like this:
```
Content-MD5: hvsmnRkNLIX24EaM7KQqIA==
```

Although it the HTTP `Content-MD5` header would be part of an HTTP response or HTTP request that would have other headers.

For example:
```
HTTP/1.1 200 OK
Content-Length: 12
Content-MD5: hvsmnRkNLIX24EaM7KQqIA==
Content-Type: text/plain

Hello world!
```

Or:
```
PUT /apple/banana/cherry.txt
Content-Length: 12
Content-MD5: hvsmnRkNLIX24EaM7KQqIA==
Content-Type: text/plain

Hello world!
```

⚠️ Although note that the HTTP `Content-MD5` header has largely been replaced by the newer HTTP `Digest`, `Want-Digest`, `Content-Digest`, `Want-Content-Digest`, `Repr-Digest`, and `Want-Repr-Digest` headers. But regardless, in this section we will focus on the `Content-MD5` header.

Your assignment is to write (so called) "middleware" that will add the appropriate `Content-MD5` header to an HTTP response.

## Assignment №8

Your assignment is to write program that —

* make an HTTP request to a URL given via `os.Args[1]`, 
* outputs the content that was downloaded to `os.Stdout`,
* look for an HTTP `Content-MD5` response header, and — 
  * if the `Content-MD5` response header doesn't exist, then output to `os.Stderr` that it cannot verify the integrity of the download file,
  * else if the `Content-MD5` response header does exist compare its value with the what the program calculates to be the MD5 digest for the content and —
    * if they are equal, output a message saying so to `os.Stderr`,
    * but if they are NOT equal, ourput a message sayhing so to `os.Stdout`.

## Assignment №9

`Content-Digest`

## Assignment №10

`Repr-Digest`

---

[⏮](../..//README.md) [⬆️](../../README.md) [⏭️](../sha-1/README.md)
