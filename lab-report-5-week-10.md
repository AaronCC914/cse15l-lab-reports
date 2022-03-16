[Back to Main Page](index.md)

# Lab Report #5 &nbsp; MORE DEBUGGG

> by Jialin Chen 03/11 2022

## Test result

* Use &nbsp; `bash script.sh > XXX.txt` to store test results

* Then &nbsp; `diff XXX1.txt XXX2.txt > Diff.txt` &nbsp; to compare the two result txt files and store the comparison output in `Diff.txt`

## Test One

### Problem in the output

Here are part of the Diff.txt:

```
212c212
< [url]
---
> []
```
Upper part corresponds to result from provided implementation, and lower part corresponds to result from my implementation.

By looking at the bash result files, we found that line 212 corresponds to test file `194.md`.

Here is the link to test markdown file `194.md`:
[test-files/194.md](https://github.com/ucsd-cse15l-w22/markdown-parse/blob/main/test-files/194.md)

The content of the file is:
 ```
 [Foo*bar\]]:my_(url) 'title (with parens)'

 [Foo*bar\]]
 ```

This format does not meet the requirement of a link in markdown file, so the expected out put should be `[]`, instead of `[url]`. The provided implementation is incorrect.

### Problem in the code

The code of provided implementation failed to exclude the case where close bracket and open parenthesis are not next to each other, which should not be regarded as a link. 

The following determining code is necessary:
```
if (nextCloseBracket != openParen - 1) {
        currentIndex = closeParen + 1;
        continue;
    }
```

## Test Two

### Problem in the output

Here are part of the Diff.txt:

```
884c886
< []
---
> [foo\(and\(bar\]
```

Upper part corresponds to result from provided implementation, and lower part corresponds to result from my implementation.

By looking at the bash result files, we found that line 212 corresponds to test file `497.md`.

Here is the link to test markdown file `497.md`:
[test-files/497.md](https://github.com/ucsd-cse15l-w22/markdown-parse/blob/main/test-files/497.md)

The content of the file is:
```
[link](foo\(and\(bar\))
```

 This format meets the requirement of a link in markdown file, so the expected output should be `[foo\(and\(bar\]', instead of `[]`. The provided implementation is incorrect.

 ### Problem in the code

 The code of provided implementation cannot correctly perform the close parenthesis search when there are more open parenthesis than close parenthesis, as shown in the following code from provided implementation:
 ```
 if(openParenCount == 0) {
          return closeParen - 1;
        }
        else {
          return -1;
        }
```

*Source: [ucsd CSE 15L wi22](https://ucsd-cse15l-w22.github.io/week/week10/#lab-report-5)*

[Back to Main Page](index.md)