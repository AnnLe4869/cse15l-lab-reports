# Lab 10 report

## Repos are used

My own repository at [https://github.com/AnnLe4869/markdown-parse](https://github.com/AnnLe4869/markdown-parse)

The other repository made by the instructor at [https://github.com/ucsd-cse15l-w22/markdown-parse](https://github.com/ucsd-cse15l-w22/markdown-parse)

## How you found the tests with different results

I first get the `result.txt` from the lab 9 repository and compare that to my own group repository using `diff` command. In particular, I run

```bash
diff -u my-result.txt other-result.txt
```

The result would look like this

```bash
--- my_results.txt      2022-03-10 09:47:39.357747200 -0800
+++ other_results.txt   2022-03-10 09:49:02.441919000 -0800
@@ -209,7 +209,7 @@
 test-files/193.md
 []
 test-files/194.md
-[]
+[url]
 test-files/195.md
 []
 test-files/196.md
@@ -227,7 +227,7 @@
 test-files/200.md
 []
 test-files/201.md
-[]
+[baz]
 test-files/202.md
 []
 test-files/203.md
@@ -539,7 +539,7 @@
 test-files/341.md
 []
 test-files/342.md
-[]
+[/foo`]
 test-files/343.md
 []
 test-files/344.md
```

From that, I can see there are difference in the result in test file `194.md` and test file `201.md` (and there are more, but let's stick with these two)

## On the first test 194.md

This is the content of the file itself

```markdown
[foo*bar\]]: my_(url) "title (with parens)"

[Foo*bar\]]
```

My own code output

```bash
[]
```

The other repo output

```bash
[url]
```

The correct answer should be

```bash
[title (with parens)]
```

So both implementation are incorrect. I think I need to watch out for special case of what is considered to be link. In particular, the part I have to fix is

```java
final String regex = "(?<!!)(?<!`)\\[(?>[[a-zA-Z0-9 ]&&[^\\n]])+\\]\\((\\S+)\\)";
```

## On the second test 201.md

This is the content of the file itself

```txt
[foo]: <bar>(baz)

[foo]
```

My own code output

```bash
[]
```

The other repo output

```bash
[baz]
```

The correct answer should be

```bash
[]
```

And my implementation is correct
