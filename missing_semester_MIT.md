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

Show nice manual and its us of a cmd:

```
$ tldr ls
```

Finding files

```
$ tldr ls
```


Finding files

```
# Find all directories named src
$ find . -name src -type d
# Find all python files that have a folder named test in their path
$ find . -path '*/test/*.py' -type f

# Delete all files with .tmp extension
$ find . -name '*.tmp' -exec rm {} \;
# Find all PNG files and convert them to JPG
$ find . -name '*.png' -exec convert {}{}.jpb \;
```

Finding in files with ripgrep

```
# Fin all python files where we imported pandas
$ rp -t py 'import pandas'
```


Finding Commnands in the shell history

```
$ history | grep touch

# ctrl+R 
```
