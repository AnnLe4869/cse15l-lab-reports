# Lab 8 report

My own repository is at [markdown-parse](https://github.com/AnnLe4869/markdown-parse)

The repository that my group review is from [QijunHuMary GitHub repo](https://github.com/QijunHuMary/markdown-parse)

## Snipper 1

The snippet used for the test

```markdown
`[a link`](url.com)

[another link](`google.com)`

[`cod[e`](google.com)

[`code]`](ucsd.edu)
```

The test for this is

```java
@Test
    public void testGetLinks1() throws IOException {
        try {
            String contents = getContentFromFile("snippet1.md");
            List<String> links = MarkdownParse.getLinks(contents);
            List<String> linksTest =
                    List.of("`google.com","google.com","ucsd.edu");
            assertEquals(linksTest, links);
        } catch (Exception e) {

        }
    }
```

---

On my own code, it fails on this snippet. The detail log

```bash
java.lang.AssertionError: 
Expected :[`google.com, google.com, ucsd.edu]
Actual   :[`google.com]
```

I may add an look-ahead checkup for the backtick, just like how I did the test on the "!" to remove the case where the link is for image. The change may look like this

```java
        // old
        final String regex = "(?<!!)(?<!`)\\[(?>[[a-zA-Z0-9 ]&&[^\\n]])+\\]\\((\\S+)\\)";
        // new
        final String regex = "(?<!!)(?<!`)\\[(?>[[a-zA-Z0-9 ]&&[^\\n]])+\\]\\((\\S+)\\)";
```

---

On other group implementation, it also fails on this snippet. The detail log

```bash
java.lang.AssertionError: 
Expected :[`google.com, google.com, ucsd.edu]
Actual   :[url.com, `google.com, google.com]
```

## Snippet 2

The snippet used for the test

```bash
[a [nested link](a.com)](b.com)

[a nested parenthesized url](a.com(()))

[some escaped \[ brackets \]](example.com)
```

The test for this snippet is

```java
    @Test
    public void testGetLinks2() throws IOException {
        try {
            String contents = getContentFromFile("snippet2.md");
            List<String> links = MarkdownParse.getLinks(contents);

            List<String> linksTest =
                    List.of("a.com","a.com(())","example.com");

            assertEquals(linksTest, links);
        } catch (Exception e) {

        }
    }
```

---

On my own code, it fails on this snippet. The detail log

```bash
java.lang.AssertionError: 
Expected :[a.com, a.com(()), example.com]
Actual   :[a.com)](b.com, a.com(())]
```

I may add an additional test to cover the case with bracket

```java
        // old
        final String regex = "(?<!!)(?<!`)\\[(?>[[a-zA-Z0-9 ]&&[^\\n]])+\\]\\((\\S+)\\)";
        // new
        final String regex = "(?<!!)(?<!`)\\[(?>[[a-zA-Z0-9 \[\]]&&[^\\n]])+\\]\\((\\S+)\\)";
```

---

On other group, they also fail on this snippet. The detail log is

```bash
java.lang.AssertionError: 
Expected :[a.com, a.com(()), example.com]
Actual   :[a.com, a.com((]
```

## Snippet 3

```bash
[this title text is really long and takes up more than 
one line

and has some line breaks](
    https://www.twitter.com
)

[this title text is really long and takes up more than 
one line](
    https://ucsd-cse15l-w22.github.io/
)


[this link doesn't have a closing parenthesis](github.com

And there's still some more text after that.

[this link doesn't have a closing parenthesis for a while](https://cse.ucsd.edu/



)

And then there's more text
```

The test for this snippet is

```java
    @Test
    public void testGetLinks3() throws IOException {
        try {
            String contents = getContentFromFile("snippet3.md");
            List<String> links = MarkdownParse.getLinks(contents);
            List<String> linksTest =
                    List.of("https://ucsd-cse15l-w22.github.io/");

            assertEquals(linksTest, links);
        } catch (Exception e) {

        }
    }
```

---

On my own code, it fails on this snippet. The detail log

```bash
java.lang.AssertionError: 
Expected :[https://ucsd-cse15l-w22.github.io/]
Actual   :[]
```

I may add an additional test to cover the case where new line at the beginning and at the end at the same time will pass while only one of them will fail. This may be challenging because I need to take into account the existence of both of them at the same time. I don't know how to do so

---

On other group, they also fail on this test. The detail log

```bash
java.lang.AssertionError: 
Expected :[https://ucsd-cse15l-w22.github.io/]
Actual   :[[https://www.twitter.com, https://ucsd-cse15l-w22.github.io/, github.com

And there's still some more text after that.

[this link doesn't have a closing parenthesis for a while](https://cse.ucsd.edu/, https://cse.ucsd.edu/]]
```