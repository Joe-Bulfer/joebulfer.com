### Overview

Python and Bash are both powerful languages and well worth learning. Before learning either, you should understand where they are and are not comparable. Unlike Bash, Python is used for data science, machine learning, and back end web development. Bash, being the default shell on Linux, can be ran directly from the terminal. If you've ever used Linux, the common "Linux" commands (historically UNIX programs)  such as `cd` or `ls` are really just writing bash directly in the terminal. This cannot be done with Python, which requires a `.py` file which must interpreted by a runtime. 

Basically, this means Bash scripts can often be more concise for simple tasks, but Python offers greater flexibility and is easier to integrate into larger projects. The two common libraries to do this are the **os** and **pathlib** library. Both serve to interact directly with you operating system, whether on Windows, Macos, or Linux. The **pathlib** is a more modern, object oriented library with more concise syntax. The **os** library is lower level with broader capabilities, such as process management and environment variable access. **pathlib** is exclusively designed for file and directory management, making it the better option.

`os.listdir` scans through the directory, and a list comprehension filters out files ending with `.md`. The `os.walk` function uses a recursive search, navigating through all sub directories. Notice how verbose and nested the function bodies of these functions are compared to **pathlib**.

### Python

#### OS Library

```python
import os

def count_md_files(directory):
    return len([f for f in os.listdir(directory) if f.endswith('.md')])

def count_md_files_rec(root_dir):
    count = 0
    for dirpath, dirnames, filenames in os.walk(root_dir):
        for filename in filenames:
            if filename.endswith('.md'):
                count += 1
    return count

option = input("Recursive? y/n >")
directory = input("Enter directory path > ")

if option == 'y':
    print("Number of .md files:", count_md_files_rec(directory))
if option == 'n':
    print("Number of .md files:", count_md_files(directory))
```

**pathlib** uses `Path().glob` for a non-recursive search and `Path().rglob` for a recursive search. Notice from the `option` assignment to the end of both files they are exactly the same. The function body is all that is different. With the **pathlib** functions, it is much more concise, with one line of code each. 

#### Pathlib Library

```python
from pathlib import Path

def count_md_files(directory):
    return sum(1 for _ in Path(directory).glob('*.md'))

def count_md_files_rec(directory):
    return sum(1 for _ in Path(directory).rglob('*.md'))

option = input("Recursive? y/n > ")
directory = input("Enter directory path > ")

if option == 'y':
    print("Number of .md files:", count_md_files_rec(directory))
elif option == 'n':
    print("Number of .md files:", count_md_files(directory))

```

### Bash

Now we have seen the python files, let's try the exact same task in Bash. As mentioned in the beginning, the fundamental difference is that Bash is not only a *language*, but also the *shell*, which is just the interface between the user and the kernel and executes programs called commands. This shell, bash being the most common, is accessed through the terminal. And through the terminal, any commands, even a series of commands at once (a script) , can be run directly in the terminal without needing to create a separate file. This means you have more direct and immediate access for troubleshooting, administration, or short tasks such as managing files, in this case, counting `.md` files.

Each of these, one counting recursive by defualt, the other with a `maxdepth` of 1, can be ran directly in the terminal, getting immediate results. We specify the `-type f` for files, as opposed to directories, or anything else. We use `-name "*.md"` to acces only files with a name that ends in `.md`, the asterisks is just a wildcard, for any character or series of characters. We then pipe `|` that output to the word count`wc` program, which despite the name, is a more general program that can count many things, including in this case, lines with the `-l` flag. 

```bash
# the find command in recursive by default
find ~/documents/sync-main/todo/ -type f -name "*.md" | wc -l
# set maxdepth 1 to only search the given directory.
find ~/documents/sync-main/todo/ -maxdepth 1 -type f -name "*.md" | wc -l
```

If we want a more interactive program that prompts a user, like the python scripts, we can `read` a variable called `option` and `directory` with a prompt specifies with the `-p` flag. Then run some basic if-else statements. If we really wanted to make it exactly like the python files, we could use functions, which Bash supports, but I found this to be more concise for this tutorial.

```bash
#!/bin/bash

read -p "Recursive? y/n > " option
read -p "Enter directory path > " directory

if [ "$option" == "y" ]; then
    find "$directory" -type f -name "*.md" | wc -l
elif [ "$option" == "n" ]; then
    find "$directory" -maxdepth 1 -type f -name "*.md" | wc -l
else
    echo "Invalid option."
fi
```

### Key Takeaways

#### Python 
- Python is used for Data Science, Machine Learning, and Backed web apps, and is only comparable to Bash for scripting purposes.
- Python offers two main libraries for file management: `os` and `pathlib`. `os` is older and has broader capabilities, while `pathlib` is modern and focuses solely on file and directory manipulation.

#### Bash

- Bash serves two roles—it's both a scripting language and the default shell for Linux. This gives it more direct access to system functionalities, allowing you to run scripts and commands directly from the terminal.

#### Conclusion

- if you can solve the problem at hand using only calls to command-line tools, you might as well use Bash. But for times when your script is part of a larger Python project, you might as well use Python.
