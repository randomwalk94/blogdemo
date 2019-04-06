---
title: "Let's 'Go'"
date: 2019-04-06T13:44:21-04:00
categories:
- coding
tags:
- coding
- golang
keywords:
- tech
thumbnailImagePosition: left
thumbnailImage: /img/golang.png
---

<progress value="0" id="progressBar">
  <div class="progress-container">
    <span class="progress-bar"></span>
  </div>
</progress>

I decided to take a look at the Go language. One of the reasons is that it shares the name with my favorite board game, Go.
<figure>
  <img src="/img/goboard.jpg" alt="my alt text"/>
  <figcaption>A Go board.</figcaption>
</figure>
<!--more-->

Of cource, the best resource to learn Go is its own [website](https://golang.org/). They also have an interactive Go text editor and compiler at [A Tour of Go](https://tour.golang.org/welcome/1). The following code demonstrates Go syntax.

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

I plan to learn Go later. It seems cool.
