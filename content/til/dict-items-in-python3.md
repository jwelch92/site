+++
title = "Dict items in Python 3"
date = 2022-12-21
+++

# TIL 12/21/2022

I was working on writing a utility to extract arbitrarily nested fields from a dictionary and found a couple of posts about the "stack of iterators" pattern.
This seemed like a good fit for the problem, and this post https://garethrees.org/2016/09/28/pattern/ even outlines this exact use case. 

However, I was having a lot of trouble getting things to work correctly. It was ending up in an infinite loop on a leaf dictionary and never hitting the exit branch. 

Compare the following

```python
def get_nested_value(
    mapping: Mapping, key: str = "value", default: Optional[str] = None
) -> Optional[str]:
    stack = [mapping.items()]
    while stack:
        for k, v in stack[-1]:
            if isinstance(v, dict):
                stack.append(v.items())
                break
            elif k == key:
                return v
        else:
            stack.pop()
    return default
```

```python
def get_nested_value(
    mapping: Mapping, key: str = "value", default: Optional[str] = None
) -> Optional[str]:
    stack = [iter(mapping.items())]
    while stack:
        for k, v in stack[-1]:
            if isinstance(v, dict):
                stack.append(iter(v.items()))
                break
            elif k == key:
                return v
        else:
            stack.pop()
    return default
```

See the bug? Turns out, this is a case where using `dict.items()` is not safe, for reasons I am still figuring out. Dict items is a view, not an iterator, so my best guess is that 
on each loop we're basically starting over instead of resuming iteration after the leaf dict was searched. All I had to do was add `iter()` around each `dict.items()` and it started working!
