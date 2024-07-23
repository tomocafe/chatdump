# chatdump

Prints file contents along with their relative locations to be pasted into an LLM-based chat program.

```
$ chatdump -b $(find my_project/ -name "*.py") | xclip
```

Enter a question into the chat prompt: 

> I'm getting the following error:
> 
> ```
> Traceback (most recent call last):
>   File "foo.py", line 3, in <module>
>     from bar import Bar
> ImportError: cannot import name 'Bar' from 'bar' (unknown location)
> ```
> 
> How do I fix it?

Then paste the output of `chatdump` into the prompt to provide context:

> Here are 2 relevant files and their locations in the project:
> 
> ```
> foo.py
> bar/bar.py
> ```
> 
> **foo.py:**
> 
> ```python
> import sys
> 
> from bar import Bar
> 
> sys.exit(Bar.BAR)
> ```
> 
> **bar/bar.py:**
> 
> ```python
> class Bar:
>     def __init__(self, num=1337):
>         self.BAR = num
> ```
> 
> Please don't include entire files in your response. Rather include only snippets of code that require highlighting or modification.

## Advanced Usage

See `chatdump --help` for all available options, but here are the highlights:

* `-r`: Set the directory to which the filenames are shown relative to (defaults to the first common ancestor)
* `-t`: Add a file to the tree listing, but don't print its contents
* `-b`: Add boilerplate to the end of the output. By default it adds the following text:

  > Please don't include entire files in your response. Rather include only snippets of code that require highlighting or modification.

* `-B`: Change the boilerplate text for this invocation
