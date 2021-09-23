---
layout: post
title: Python Tips
tags: [python]
---

- Using `__slots__ = ()` inside a class will prevent its attributes to be changed. [[ref](https://stackoverflow.com/a/23274028)]
- Only for Python3, 3 different types of raising Exception:
  1. Normal Exception (Not expected to have another exception while handling an exception)
    ```python
    try: raise Exception("Error")
    except Exception as e: raise Exception("Error while handling Exception")
    ```
  2. Cause of Exception (The second exception is expected to happen while handling an exception)
    ```python
    try: raise Exception("Error")
    except Exception as e: raise Exception("Different Exception") from e
    ```
  3. Only show last Exception (Ignoring the first exception)
    ```python
    try: raise Exception("Error")
    except Exception as e: raise Exception("Different error") from None
    ```
