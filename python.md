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

#### Dijkstra's algorithm in Python

```python
#  Dijkstra's algorithm in python
#
#  As others have pointed out, due to not using understandable variable
#  names, it is almost impossible to debug your code.
#
#  Following the wiki article about Dijkstra's algorithm, one can
#  implement it along these lines (and in a million other manners):

nodes = ('A', 'B', 'C', 'D', 'E', 'F', 'G')
distances = {
    'B': {'A': 5, 'D': 1, 'G': 2},
    'A': {'B': 5, 'D': 3, 'E': 12, 'F' :5},
    'D': {'B': 1, 'G': 1, 'E': 1, 'A': 3},
    'G': {'B': 2, 'D': 1, 'C': 2},
    'C': {'G': 2, 'E': 1, 'F': 16},
    'E': {'A': 12, 'D': 1, 'C': 1, 'F': 2},
    'F': {'A': 5, 'E': 2, 'C': 16}}

unvisited = {node: None for node in nodes} #using None as +inf
visited = {}
current = 'B'
currentDistance = 0
unvisited[current] = currentDistance

while True:
    for neighbour, distance in distances[current].items():
        if neighbour not in unvisited: continue
        newDistance = currentDistance + distance
        if unvisited[neighbour] is None or unvisited[neighbour] > newDistance:
            unvisited[neighbour] = newDistance
    visited[current] = currentDistance
    del unvisited[current]
    if not unvisited: break
    candidates = [node for node in unvisited.items() if node[1]]
    current, currentDistance = sorted(candidates, key = lambda x: x[1])[0]

print(visited)

#  This code is more verbous than necessary and I hope comparing your
#  code with mine you might spot some differences.
#
#  The result is:

{'E': 2, 'D': 1, 'G': 2, 'F': 4, 'A': 4, 'C': 3, 'B': 0}
```

