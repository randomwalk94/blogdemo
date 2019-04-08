---
title: "Let's 'Go'"
date: 2019-04-06T13:44:21-04:00
categories:
- coding
tags:
- golang
keywords:
- tech
thumbnailImagePosition: left
thumbnailImage: /img/golang.png
---
I decided to take a look at the Go language. One of the reasons is that it shares the name with my favorite board game, Go.
<figure>
  <img src="/img/goboard.jpg" alt="my alt text"/>
  <figcaption>A Go board.</figcaption>
</figure>
<!--more-->

Of cource, the best resource to learn Go is its own [website](https://golang.org/). They also have an interactive Go text editor and compiler at [A Tour of Go](https://tour.golang.org/welcome/1). The following code demonstrates Go's *C*-like syntax.

{{< codeblock "A simple Go program." "go" "https://tour.golang.org/welcome/4" "sandbox.go" >}}
package main

import (
	"fmt"
	"time"
)

func main() {
	fmt.Println("Welcome to the playground!")

	fmt.Println("The time is", time.Now())
}
{{< /codeblock >}}

The code uses two packages `fmt` which implements I/O and `time` which provides time functionality.  

Go has gained more popularity in the development world, especially in back-end environment. Developed by Google, it was created to solve [many problems](https://hackernoon.com/the-beauty-of-go-98057e3f0a7d) faced by the search giant. This blog is also  written by [Hugo framework](https://gohugo.io/), which is a product of Go.  

Here is an introduction to Go using hands-on examples: [gobyexample](https://gobyexample.com/).  

I did a little research and dug into Go source code by
```
cd /usr/local/go/pkg
```
Then went inside the `math` package and found several functions such as `sin.go` and `log.go`. What are the algorithms does Go use to implement these common functions? First guess would be using Taylor expansion. It is indeed the case, but with some additional magic. Apparently, these functions are re-implemented by using their *C* versions. For example, here is the content at the beginning of `log.go`:

{{< codeblock "logarithm function in Go." "go" "https://golang.org/src/math/log.go" "log.go" >}}
// Copyright 2009 The Go Authors. All rights reserved.
// Use of this source code is governed by a BSD-style
// license that can be found in the LICENSE file.

package math

/*
	Floating-point logarithm.
*/

// The original C code, the long comment, and the constants
// below are from FreeBSD's /usr/src/lib/msun/src/e_log.c
// and came with this notice. The go code is a simpler
// version of the original C.
//
// ====================================================
// Copyright (C) 1993 by Sun Microsystems, Inc. All rights reserved.
//
// Developed at SunPro, a Sun Microsystems, Inc. business.
// Permission to use, copy, modify, and distribute this
// software is freely granted, provided that this notice
// is preserved.
// ====================================================
//
// __ieee754_log(x)
// Return the logarithm of x
{{</codeblock>}}

The interesting part is what follows:

{{< codeblock "Remez algorithm" "go" "https://golang.org/src/math/log.go" "log.go" >}}

// Method :
//   1. Argument Reduction: find k and f such that
//			x = 2**k * (1+f),
//	   where  sqrt(2)/2 < 1+f < sqrt(2) .
//
//   2. Approximation of log(1+f).
//	Let s = f/(2+f) ; based on log(1+f) = log(1+s) - log(1-s)
//		 = 2s + 2/3 s**3 + 2/5 s**5 + .....,
//	     	 = 2s + s*R
//      We use a special Remez algorithm on [0,0.1716] to generate
//	a polynomial of degree 14 to approximate R.  The maximum error
//	of this polynomial approximation is bounded by 2**-58.45. In
//	other words,
//		        2      4      6      8      10      12      14
//	    R(z) ~ L1*s +L2*s +L3*s +L4*s +L5*s  +L6*s  +L7*s
//	(the values of L1 to L7 are listed in the program) and
//	    |      2          14          |     -58.45
//	    | L1*s +...+L7*s    -  R(z) | <= 2
//	    |                             |
//	Note that 2s = f - s*f = f - hfsq + s*hfsq, where hfsq = f*f/2.
//	In order to guarantee error in log below 1ulp, we compute log by
//		log(1+f) = f - s*(f - R)		(if f is not too large)
//		log(1+f) = f - (hfsq - s*(hfsq+R)).	(better accuracy)
//
//	3. Finally,  log(x) = k*Ln2 + log(1+f).
//			    = k*Ln2_hi+(f-(hfsq-(s*(hfsq+R)+k*Ln2_lo)))
//	   Here Ln2 is split into two floating point number:
//			Ln2_hi + Ln2_lo,
//	   where n*Ln2_hi is always exact for |n| < 2000.
//

{{< /codeblock >}}

The same goes for `sin.go`. The tool being used here is called Remez algorithm. More information is available at its [Wikipedia page](https://en.wikipedia.org/wiki/Remez_algorithm). Here is just a snippet:

> The **Remez algorithm** or **Remez exchange algorithm**, published by Evgeny Yakovlevich Remez in 1934, is an iterative algorithm used to find simple approximations to functions, specifically, approximations by functions in a Chebyshev space that are the best in the uniform norm $L\_\infty$ sense.

