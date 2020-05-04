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

