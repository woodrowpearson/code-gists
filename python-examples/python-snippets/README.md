# Python Snippets

### Count all uppercase letters in a file.

```python
with open('./test_text.txt') as fh:
	count = sum(1 for c in fh.read() if c.isupper())
	print("The # of capital letters in file", str(count))
```

#### Implement a stack with 2 queues

{% code title="two\_stacks\_queue.py" %}
```python
#  Implement A Queue using Two Stacks Python

class Queue(object):
    def __init__(self):
        self.instack=[]
        self.outstack=[]
    def enqueue(self,element):
        self.instack.append(element)
    def dequeue(self):
        if not self.outstack:
            while self.instack:
                self.outstack.append(self.instack.pop())
        return self.outstack.pop()
q=Queue()
for i in range(10):
    q.enqueue(i)
for i in xrange(10):
    print q.dequeue(),
```
{% endcode %}

#### Check for duplicate files

{% code title="checkDuplicates.py" %}
```python
#  # Fastest algorithm - 100x performance increase compared to the
#  accepted answer (really :))
#  The approaches in the other solutions are very cool, but they forget
#  about an important property of duplicate files - they have the same
#  file size. Calculating the expensive hash only on files with the same
#  size will save tremendous amount of CPU; performance comparisons at
#  the end, here's the explanation.
#
#  Iterating on the solid answers given by @nosklo and borrowing the idea
#  of @Raffi to have a fast hash of just the beginning of each file, and
#  calculating the full one only on collisions in the fast hash, here are
#  the steps:
#
    #  1. Buildup a hash table of the files, where the filesize is the
#  key.
    #  2. For files with the same size, create a hash table with the hash
#  of their first 1024 bytes; non-colliding elements are unique
    #  3. For files with the same hash on the first 1k bytes, calculate
#  the hash on the full contents - files with matching ones are NOT
#  unique.
#  The code:

#!/usr/bin/env python
import sys
import os
import hashlib

def chunk_reader(fobj, chunk_size=1024):
    """Generator that reads a file in chunks of bytes"""
    while True:
        chunk = fobj.read(chunk_size)
        if not chunk:
            return
        yield chunk

def get_hash(filename, first_chunk_only=False, hash=hashlib.sha1):
    hashobj = hash()
    file_object = open(filename, 'rb')

    if first_chunk_only:
        hashobj.update(file_object.read(1024))
    else:
        for chunk in chunk_reader(file_object):
            hashobj.update(chunk)
    hashed = hashobj.digest()

    file_object.close()
    return hashed

def check_for_duplicates(paths, hash=hashlib.sha1):
    hashes_by_size = {}
    hashes_on_1k = {}
    hashes_full = {}
    
    for path in paths:
        for dirpath, dirnames, filenames in os.walk(path):
            for filename in filenames:
                full_path = os.path.join(dirpath, filename)
                try:
                    # if the target is a symlink (soft one), this will
                    # dereference it - change the value to the actual target file
                    full_path = os.path.realpath(full_path)
                    file_size = os.path.getsize(full_path)
                except (OSError,):
                    # not accessible (permissions, etc) - pass on
                    continue

                duplicate = hashes_by_size.get(file_size)

                if duplicate:
                    hashes_by_size[file_size].append(full_path)
                else:
                    hashes_by_size[file_size] = []  # create the list for this file size
                    hashes_by_size[file_size].append(full_path)

    # For all files with the same file size, get their hash on the 1st 1024 bytes
    for __, files in hashes_by_size.items():
        if len(files) < 2:
            continue    # this file size is unique, no need to spend cpy cycles on it

        for filename in files:
            try:
                small_hash = get_hash(filename, first_chunk_only=True)
            except (OSError,):
                # the file access might've changed till the exec point got here
                continue

            duplicate = hashes_on_1k.get(small_hash)
            if duplicate:
                hashes_on_1k[small_hash].append(filename)
            else:
                hashes_on_1k[small_hash] = []          # create the list for this 1k hash
                hashes_on_1k[small_hash].append(filename)

    # For all files with the hash on the 1st 1024 bytes, get their hash on the full file - collisions will be duplicates
    for __, files in hashes_on_1k.items():
        if len(files) < 2:
            continue    # this hash of fist 1k file bytes is unique, no need to spend cpy cycles on it

        for filename in files:
            try:
                full_hash = get_hash(filename, first_chunk_only=False)
            except (OSError,):
                # the file access might've changed till the exec point got here
                continue

            duplicate = hashes_full.get(full_hash)
            if duplicate:
                print "Duplicate found: %s and %s" % (filename, duplicate)
            else:
                hashes_full[full_hash] = filename

if sys.argv[1:]:
    check_for_duplicates(sys.argv[1:])
else:
    print "Please pass the paths to check as parameters to the script"

#  And, here's the fun part - performance comparisons.
#
#  Baseline -
#
    #  * a directory with 1047 files, 32 mp4, 1015 - jpg, total size -
#  5445.998 MiB - i.e. my phone's camera auto upload directory :)
    #  * small (but fully functional) processor - 1600 BogoMIPS, 1.2 GHz
#  32L1 + 256L2 Kbs cache, /proc/cpuinfo:
> Processor       : Feroceon 88FR131 rev 1 (v5l)
> BogoMIPS        : 1599.07

#  (i.e. my low-end NAS :), running Python 2.7.11.
#
#  So, the output of @nosklo's very handy solution:

root@NAS:InstantUpload# time ~/scripts/checkDuplicates.py
```
{% endcode %}

#### Read JSON file

```python
#  Then you can use your code:

import json
from pprint import pprint

with open('data.json') as f:
    data = json.load(f)

pprint(data)

#  With data, you can now also find values like so:

data["maps"][0]["id"]
data["masks"]["id"]
data["om_points"]
```

#### Return nth Fibonacci sequence

```python
#  Fibonacci numbers, with an one-liner in Python 3?
from functools import reduce

fib = lambda n:reduce(lambda x,n:[x[1],x[0]+x[1]], range(n),[0,1])[0]

#  (this maintains a tuple mapped from [a,b] to [b,a+b], initialized to
#  [0,1], iterated N times, then takes the first tuple element)

fib(1000)
43466557686937456435688527675040625802564660517371780402481729089536555417949051
89040387984007925516929592259308032263477520968962323987332247116164299644090653
3187938298969649928516003704476137795166849228875L

#  (note that in this numbering, fib(0) = 0, fib(1) = 1, fib(2) = 1,
#  fib(3) = 2, etc.)
#
#  (also note: reduce is a builtin in Python 2.7 but not in Python 3;
#  you'd need to execute from functools import reduce in Python 3.)
```

#### Minimum Window Substring

```python
#  find Minimum Window Substring
#
#  Assume that String S and T only contains A-Z characters (26
#  characters)
#
    #  * First, create an array count, which store the frequency of each
#  characters in T.
    #  * Process each character in S, maintaining a window l, r, which
#  will be the current minimum window that contains all characters in T.
    #  * We maintain an array cur to store the current frequency of
#  characters in window. If the frequency of the character at the left
#  end of the window is greater than needed frequency, we increase l
#
#  Sample Code:

    int[]count = new int[26];
    for(int i = 0; i < T.length; i++)
        count[T[i] - 'A']++;

    int need = 0;//Number of unique characters in T
    for(int i = 0; i < 26; i++)
        if(count[i] > 0)
           need++;
    int l = 0, r = 0;
    int count = 0;
    int result ;
    int[]cur = new int[26];
    for(int i = 0; i < S.length; i++){
         cur[S[i] - 'A']++;
         r = i;
         if(cur[S[i] - 'A'] == count[S[i] - `A`]){
             count++;
         }
         //Update the start of the window,
         while(cur[S[l] - 'A'] > count[S[l] - 'A']){
               cur[S[l] - 'A']--;
               l++;
         }
         if(count == need)
             result = min(result, r - l + 1);
    }

#  Each character in S will be processed at most two times, which give us
#  O(n) complexity.
```

#### Rainwater Problem

```python
#  Calculate trapped water in a structure
#
#  This can be solved in linear time with linear memory requirements in
#  the following way:

def answer(heights):
    minLeft = [0] * len(heights)
    left = 0
    for idx, h in enumerate(heights):
        if left < h:
            left = h
        minLeft[idx] = left

    minRight = [0] * len(heights)
    right = 0
    for idx, h in enumerate(heights[::-1]):
        if right < h:
            right = h
        minRight[len(heights) - 1 - idx] = right

    water = 0
    for h, l, r in zip(heights, minLeft, minRight):
        water += min([l, r]) - h

    return water

#  The arrays minLeft and minRight contain the highest level at which
#  water can be supported at a place in the array if there was a wall of
#  infinite size on the right or left side respectively. Then at each
#  index, total water that can be contained is the minimum of the water
#  levels supported by the left and the right side - height of the floor.
#
#  This question deals with this problem in higher dimension (relating it
#  to the Watershed problem in image processing):
#  https://stackoverflow.com/questions/21818044/the-maximum-volume-of-
#  trapped-rain-water-in-3d
```

#### House Robber Problem

```python
#  Issue with memoization - House Robber problem
#
#  Your approach for memoization won't work because when you reach some
#  index i, if you've already computed some result for i, your algorithm
#  fails to consider the fact that there might be a better result
#  available by robbing a more optimal set of houses in the left portion
#  of the array.
#
#  The solution to this dilemma is to avoid passing the running value
#  (money you've robbed) downward through the recursive calls from
#  parents to children. The idea is to compute sub-problem results
#  without any input from ancestor nodes, then build the larger solutions
#  from the smaller ones on the way back up the call stack.
#
#  Memoization of index i will then work because a given index i will
#  always have a unique set of subproblems whose solutions will not be
#  corrupted by choices from ancestors in the left portion of the array.
#  This preserves the optimal substructure that's necessary for DP to
#  work.
#
#  Additionally, I recommend avoiding global variables in favor of
#  passing your data directly into the function.

def maximize_robberies(houses, memo, i=0):
    if i in memo:
        return memo[i]
    elif i >= len(houses):
        return 0

    memo[i] = max(
        houses[i] + maximize_robberies(houses, memo, i + 2),
        maximize_robberies(houses, memo, i + 1)
    )
    return memo[i]

print(maximize_robberies([1, 2, 1, 1], {}))
```

#### URL shortener example

```python
  def generate_random_slug():
    global current_random_slug_id
    while True:
        slug = base_conversion(current_random_slug_id, base_62_alphabet)
        current_random_slug_id += 1
        # Make sure the slug isn't already used
        existing = DB.get({'slug': slug})
        if not existing:
            return slug
            

## Using the actual bit.ly package

from bitlyshortener import Shortener

tokens_pool = ['bitly_general_access_token']  # Use your own.
shortener = Shortener(tokens=tokens_pool, max_cache_size=128)

@usr_account.route("/account/createtable", methods=["POST"])
def account_createtable():
    form = CreateTableForm(request.form)
    if form.validate():
        tableid = DB.add_table(form.tablenumber.data, current_user.get_id())
        new_urls = [f'{config.base_url}newrequest/{tableid}']
        short_url = shortener.shorten_urls(new_urls)[0]
        DB.update_table(tableid, short_url)
        return redirect(url_for('account.account'))
    return render_template("account.html", createtableform=form, tables=DB.get_tables(current_user.get_id()))
```

#### Multiple Hash Function

```python
#  ## Consider using dataclasses
#  For most objects you write __hash__ functions for, you actually want
#  to be using a dataclass generated class
#  (https://docs.python.org/3.7/library/dataclasses.html):

from dataclasses import dataclass
from typing import Union

@dataclass(frozen=True)
class Foo:
    a: Union[int, str]
    b: Union[int, str]
```

