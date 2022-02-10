# Lab 4 report

## Table of content

- [Test file used](#test-file-used)
- [First code change](#first-code-change)
- [Second code change](#second-code-change)
- [Third code change](#third-code-change)

## First code change

**Initial behavior**: when use this test file as input, the program enter an infinite loop. We must force the program to terminate to exit this loop

**Test file**: we use [this test file](test-file1.md)

**Expected behavior**: the program print out

    ```bash
    [https://something.com, some-page.html]
    ```

**Brief description of the change**: I added check statement to see whether the first search return -1 or not. If it return -1 we shall stop the while loop

![Second code change](first-code-change.png)

**Actual output**: actually work, no longer has infinite loop. In fact, this is very close to our expected output

![code output after the second change](first-output.png)

**Explanation**: the `indexOf` return -1 if it cannot find the sequence. This will make the caret go backward instead of going forward if we still have some content after the last "link". I fixed this behavior by adding a check on the first search so that, if it cannot find the first parenthesis, it means no more link exist and the program shall stop

## Second code change

**Initial behavior**: when use this test file as input, the program enter an infinite loop

**Test file**: we use [this test file](test-file2.md)

**Expected behavior**: the program print out

    ```bash
    null
    ```

**Brief description of the change**: I added check statement to see whether the first search return -1 or not. If it return -1 we shall stop the while loop

![Second code change](second-code-change.png)

**Actual output**: actually work, no longer has infinite loop. In fact, this is very close to our expected output

![code output after the second change](second-output.png)

**Explanation**: the `indexOf` return -1 if it cannot find the sequence. This will make the caret go backward instead of going forward if we still have some content after the last "link". I fixed this behavior by adding a check on the ALL search so that, if it cannot find the sequence, it means no more link exist and the program shall stop

## Third code change

**Initial behavior**: when use this test file as input, the program print out the link of the image, which we don't want

**Test file**: we use [this test file](test-file3.md)

**Expected behavior**: the program print out

    ```bash
    https://hello.com
    ```

**Brief description of the change**: I use the regular expression

![Third code change](third-code-change.png)

**Actual output**: work for the sample test 3 [test-file3.md] but fail other test file.

![code output after the third change](third-output.png)

**Explanation**: probably have something to do with the way Java handle regular expression, especially with the grouping mechanic. I test this same regular expression with Javascript on [regexr](https://regexr.com/)
