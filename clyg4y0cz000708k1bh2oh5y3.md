---
title: "Day 4 [part :- 3] :- 🔍 Mastering Text Processing in Ubuntu: grep, find, awk, and sed 🚀"
seoTitle: "Master Text Processing in Ubuntu"
seoDescription: "Master text processing in Ubuntu with `grep`, `find`, `awk`, and `sed` commands for searching, processing, and manipulating text in the CLI"
datePublished: Wed Jul 10 2024 17:50:09 GMT+0000 (Coordinated Universal Time)
cuid: clyg4y0cz000708k1bh2oh5y3
slug: day-4-part-3-mastering-text-processing-in-ubuntu-grep-find-awk-and-sed
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1720633694485/94575e55-80f5-4041-9253-2389f8f570b3.png
ogImage: https://cdn.hashnode.com/res/hashnode/image/upload/v1720633799760/7ea04727-252f-42a7-9d40-3f47a3ede62f.png
tags: ubuntu, devops, devops-articles, 90daysofdevops, trainwithshubham

---

The `grep`, `find`, `awk`, and `sed` commands are powerful tools in the Ubuntu command line interface (CLI) used for searching, processing, and manipulating text. Here's an explanation of each:

### `grep`

`grep` (Global Regular Expression Print) is used to search for specific patterns within files. It supports regular expressions, making it a versatile tool for pattern matching.

**Basic Usage:**

```bash
grep 'pattern' filename

#for multiple
grep "pattern" filename1 filename2

#for printing with line number
grep -n "pattern" filename
```

**Example:**

```bash
grep 'hello' file.txt
```

This command searches for the word "hello" in `file.txt`.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1720617138230/c39d5039-016a-4a41-9e75-a74b59bac6fa.png align="center")

### `find`

`find` is used to search for files and directories within a directory hierarchy. It can search by name, type, size, modification time, and more.

**Basic Usage:**

```bash
find [path] [expression]
```

**Example:**

```bash
find /home/user -name "*.txt"
```

This command searches for all `.txt` files in the `/home/user` directory.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1720632541189/044bd0a8-6801-450c-991d-7109433a858e.png align="center")

### `awk`

`awk` is a powerful programming language for pattern scanning and processing. It is used for manipulating data and generating reports.

**Basic Usage:**

```bash
awk 'pattern {action}' filename
```

**Example:**

```bash
awk '{print $1}' file.txt

#for multiple

awk '{print $1,$2,...}' file.txt
```

This command prints the first column of each line in `file.txt`.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1720632847596/d90123b0-343d-4c40-a746-5d86ff3a0191.png align="center")

### `sed`

`sed` (Stream Editor) is used for parsing and transforming text. It can perform basic text transformations on an input stream (a file or input from a pipeline).

**Basic Usage:**

```bash
sed 's/pattern/replacement/g' filename
#g means global and you can use also number , like how many time you want to change it
```

**Example:**

```bash
sed 's/hello/world/' file.txt
```

This command replaces the first occurrence of "hello" with "world" in each line of `file.txt`.

These commands are essential for text processing and file management in the Ubuntu CLI, providing robust functionality for a variety of tasks.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1720633396786/3b5a1eea-2302-407c-9f0a-8c7f4bcbe16e.png align="center")

Thank you for reading!

<mark>© 2024 Anand Raval. All rights reserved.</mark>