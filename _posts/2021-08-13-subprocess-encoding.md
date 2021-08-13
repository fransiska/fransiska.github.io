---
layout: post
title: Subprocess without shell
tags: [python]
---

I was googling for hours and I found no answer. I was also not really sure where the error happens. I found the mistake after I wrote about the problem.

### The problem

I'm trying to call ledger-cli using subprocess, preferably without `shell=True` because [it's not a good practice](https://stackoverflow.com/a/36299483). However I stumble on encoding error. The command may have a Japanese character, but I think the problem happens regardless of this.

1. Works
    ```python
    res = subprocess.run(" ".join(command), capture_output=True, encoding="utf8", universal_newlines=True, shell=True)
    ```
2. Works, need to `decode.("utf8")` the stdout
    ```python
	res = subprocess.run(" ".join(command), capture_output=True)
    ```
3. Error at ledger-cli when trying to parse the argument, the character was passed to ledger-cli as bytes if it contains Japanese character, or `"While parsing value expression: ((account =~ /expr/) | (account =~ /comment=~/a//)) Error: Invalid token '<ident 'a'>' (wanted ')')"` when it's just alphanumeric
    ```python
	res = subprocess.run(command, capture_output=True)
    ```
4. Same as (3) if the input is alphanumeric only, but when it has Japanese characters, it has these error
    ```python
	res = subprocess.run(command, capture_output=True, encoding="utf8", universal_newlines=True)
	```
	```bash
    Traceback (most recent call last):
      File "ledger.py", line 32, in <module>
        res = subprocess.run(command, capture_output=True, encoding="utf8") #UnicodeDecodeError: 'utf-8' codec can't decode byte 0xe3 in position 164: invalid continuation byte
      File "/Users/fransiska/.pyenv/versions/3.7.3/lib/python3.7/subprocess.py", line 474, in run
        stdout, stderr = process.communicate(input, timeout=timeout)
      File "/Users/fransiska/.pyenv/versions/3.7.3/lib/python3.7/subprocess.py", line 939, in communicate
        stdout, stderr = self._communicate(input, endtime, timeout)
      File "/Users/fransiska/.pyenv/versions/3.7.3/lib/python3.7/subprocess.py", line 1725, in _communicate
        self.stderr.errors)
      File "/Users/fransiska/.pyenv/versions/3.7.3/lib/python3.7/subprocess.py", line 816, in _translate_newlines
        data = data.decode(encoding, errors)
    UnicodeDecodeError: 'utf-8' codec can't decode byte 0xe3 in position 158: invalid continuation byte	
	```

The Mac OS's encoding should be utf8 since (1) works well, and the output in (2) can be decoded using utf8. But for some reason, even if I pass `encoding="utf8"` in (4) it doesn't pass the argument correctly, and also doesn't decode the error message correctly. Something in the `shell=True` fix this encoding, or maybe it's the argument passing.

### The mistake

> No need quotes for multiple words in a single list item

I was trying to call `ledger reg "expr" "comment =~ /keyword/"`. I was suspicious with the double slash in the error message when the keyword is alphanumeric, suggesting that the encoding doesn't work even in this case. Maybe some of the symbols is causing it to get encoded weirdly.

In the end, it was the quotes in the `"expr"` that was causing the problem. Not sure why, but I think subprocess automatically handle the quotes when the item inside the command has space. Like [this](https://stackoverflow.com/a/36380734). I should've known how to use subprocess better.

I guess I had too many problems with encoding that that's the one that I suspect first. :sweat:
