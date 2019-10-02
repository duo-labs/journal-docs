---
title: Features
authors:
- jwright
tags:
- features
- theme
date: 2019-09-09T21:57:00
---

When we created Journal, we knew we wanted the reading experience to be pleasant. This is why we've combined, adapted, and improved existing Hugo themes such as  the excellent [Casper](https://themes.gohugo.io/casper/) and [Academic](https://themes.gohugo.io/academic/) themes into a powerful theme.

This guide demonstrates just some of the ways you can use Journal to write and share information.

<!--more-->


## Syntax Highlighting

Journal supports full syntax highlighting! Just look at this completely factual code snippet.

```go
package main

import "fmt"

func() main{
    fmt.Println("Go is better than Rust.")
}
```

Here's a list of the languages that are supported.

## LaTEX Support

We support LaTEX (through MathJax), too! Here's a fancy equation:

$$
\[ \frac{\partial u}{\partial t}
   = h^2 \left( \frac{\partial^2 u}{\partial x^2}
      + \frac{\partial^2 u}{\partial y^2}
      + \frac{\partial^2 u}{\partial z^2} \right) \]
$$

You can also do inline math like this $x^2+1$. There are a few gotchas to consider, which you can find here.

## Google Docs Support

Hugo has the magic power of _shortcodes_, which are just HTML templates you can pass data to. There are some handy ones, including one to embed Google Docs!

Check this out:

{{< gdocs src="https://docs.google.com/document/d/1yT0ji-MT1HrrZni84BY2c6oAmQ11ntIzPndhBnJTrwc/edit?usp=sharing" >}}

## Sidenotes

{{% sidenote %}}
This is an example sidenote. You can use it to add additional background information that may not be crucial to the post.
{{% /sidenote %}}

When writing a post, you're generally trying to tell a story about a particular topic. There may be instances where you want to give some background information but don't want to take away focus from the core message.

To solve that problem, you can use the `sidenote` shortcode like this:

```
{{%/* sidenote */%}}
My note goes here.
{{%/* /sidenote */%}}
```

## Notes, Warnings, and Tips

Sometimes you want to call something out as a helpful tip, a warning, or maybe just some additional information to be aware of.

To that end, I've created the `notice` shortcode. You can use it like this:

```
{{%/* notice type */%}}
My note goes here.
{{%/* /notice */%}}
```

The `type` can be `tip`, `warning`, `info`, or `note`. Here are some examples:

{{% notice tip %}}
This is a tip!
{{% /notice %}}

{{% notice warning %}}
This is a warning!
{{% /notice %}}

{{% notice info %}}
This is just some info that might be helpful.
{{% /notice %}}

{{% notice note %}}
This is just some info that you might like!
{{% /notice %}}

## Diagrams

We often have to explain some concepts in our notes that is best left to a diagram. To that end, I've added a `mermaid` shortcode which uses the [mermaid](https://mermaidjs.github.io/) Javascript library to create a diagram using a simple grammar.

Here's an example of what the shortcode would look like:

```
{{%/* mermaid */%}}
graph TD;
    A-->B;
    A-->C;
    B-->D;
    C-->D;
{{%/* /mermaid */%}}
```

And here's the result:

{{< mermaid >}}
graph TD;
    A-->B;
    A-->C;
    B-->D;
    C-->D;
{{< /mermaid >}}