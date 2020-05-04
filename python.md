# Python

#### Open file

```python
# read file line by line
with open('filename') as f:
    content = f.readlines()
```

```python
# Iterate over list
for i, _ in enumerate(nums):
  ..
```



> ### Description
>
> Functions allow us to package together lines of code to make a process of some kind repeatable action. If there is ever a workflow that we might want to do more than once, then gathering that workflow into a function might be a good idea. In this hands-on lab, we'll be working through exercises to demonstrate creating functions that will receive arguments and return results that meet our expectations.

```python
###
The first few tasks require us to create the split_names function to take a string and split it into the first and last name, returning a dictionary with the first_name and last_name keys.

We'll modify the function to get each of the assert statements that utilize this, so let's write the implementation to get the initial assertion to succeed:

testing-functions.py
###

# 1) Write a `split_name` function that takes a string and returns a dictionary with first_name and last_name

def split_name(name):
    names = name.split()
    first_name = names[0]
    last_name = names[-1]
    return {
        'first_name': first_name,
        'last_name': last_name,
    }

assert split_name("Kevin Bacon") == {
    "first_name": "Kevin",
    "last_name": "Bacon",
}, f"Expected {{'first_name': 'Kevin', 'last_name': 'Bacon'}} but received {split_name('Kevin Bacon')}"

# 1) Write a `split_name` function that takes a string and returns a dictionary with first_name and last_name

def split_name(name):
    first_name, last_name = name.split(maxsplit=1)
    return {
        'first_name': first_name,
        'last_name': last_name,
    }

assert split_name("Kevin Bacon") == {
    "first_name": "Kevin",
    "last_name": "Bacon",
}, f"Expected {{'first_name': 'Kevin', 'last_name': 'Bacon'}} but received {split_name('Kevin Bacon')}"

# 2) Ensure that `split_name` can handle multi-word last names

assert split_name("Victor Von Doom") == {
    "first_name": "Victor",
    "last_name": "Von Doom",
}, f"Expected {{'first_name': 'Victor', 'last_name': 'Von Doom'}} but received {split_name('Victor Von Doom')}"

```

{% tabs %}
{% tab title="Test1.py" %}
```python
# 3) Write an `is_palindrome` function to check if a string is a palindrome (reads the same from left-to-right and right-to-left)

def is_palindrome(item):
    return item == item[::-1]

assert is_palindrome("radar") == True, f"Expected True but got {is_palindrome('radar')}"
assert is_palindrome("stop") == False, f"Expected False but got {is_palindrome('stop')}"
```
{% endtab %}

{% tab title="test2.py" %}
```python
# 4) Make `is_palindrome` work with numbers

assert is_palindrome(101) == True, f"Expected True but got {is_palindrome(101)}"
assert is_palindrome(10) == False, f"Expected False but got {is_palindrome(10)}"
```
{% endtab %}

{% tab title="test3.py" %}
    testing-functions.py (partial)

    # 5) Write a `build_list` function that takes an item and a number to include in a list

    def build_list(item, count=1):
        items = []
        for _ in range(count):
            items.append(item)
        return items

    assert build_list("Apple", 3) == [
        "Apple",
        "Apple",
        "Apple",
    ], f"Expected ['Apple', 'Apple', 'Apple'] but received {repr(build_list('Apple', 3))}"
    assert build_list("Orange") == [
        "Orange"
    ], f"Expected ['Orange'] but received {repr(build_list('Orange'))}"
{% endtab %}
{% endtabs %}

