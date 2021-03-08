---
title: "How to install Elixir on Linux Mint 20"
date: "2020-12-18"
categories: 
  - "english"
  - "software"
tags: 
  - "elixir"
  - "linux-mint"
---

Since last weekend I'm using Linux Mint 20 instead of Windows 10. Today, I tried to install Elixir using the Ubuntu instructions using _apt get_, without success.

So I went with the package approach:

1. Direct download from Erlang Solutions ([link](https://www.erlang-solutions.com/resources/download.html))
2. Installation of the deb files using the software manager

In details, download Erlang and Elixir for Ubuntu Focal (20.04) which is the version used by Linux Mint 20.

![](images/image-2-1024x622.png)

Open each deb file and install it with software manager:

![](images/esl-erlang.png)

![](images/elixir-1.png)

To confirm it is working OK, open a terminal and type `elixir -v`:

Easy-peasy.

![](images/image-1.png)
