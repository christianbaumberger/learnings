# My Learnings From the Course "The Missing Semester of Your CS Education"

Link: [https://missing.csail.mit.edu/](https://missing.csail.mit.edu/)

## Bash

Open the man page of ls

```
$ man ls
```

Clear prompt and screen:

```
$ ctrl l
```

Stream to file:

```
$ echo "Hello world" > test_file.txt
```

Append to file:

```
$ echo "Hello World" >> test_file.txt
```

Tail and Head:

```
$ tail -n1 test_file.txt
$ head -n1 test_file.txt
```

Pipe:

```
$ ls -la / | tail -n1
```

Open any file with its corresponding program:

```
$ xdg-open anydocument.pdf
```
