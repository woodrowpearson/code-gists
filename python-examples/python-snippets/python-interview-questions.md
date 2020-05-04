---
description: Infra/SRE focuse
---

# Python Interview Questions

## Dictionary File Problem

{% hint style="info" %}
Suppose that you have a dictionary file that has words separated by a single whitespace, kept in sorted order. So for instance, if you had three words in your dictionary, "dog", "cat", and "horse", your dictionary file would look like:

cat dog horse

1. Implement a function exists that indicates whether an argument passed in dictionary.

def exists\(word, filename\): """Returns true iff word is part of the dictionary represented by filename"""

1. If you could modify the format of this file to support more efficient lookups, what would you change about the file format?
2. Compound words are words that are composed of other words. Using the exists\(\) function you implemented earlier, implement a function that indicates whether a word is a compound word.

def is\_compound\(word, filename\): """Returns true iff word is a compound word"""

So, for example, if you have the same dictionary as indicated above, the following invocations of is\_compound should return the following values:

is\_compound\('catdog', dictionary\_file\) -&gt; True is\_compound\('dogcat', dictionary\_file\) -&gt; True is\_compound\('catdoghorse', dictionary\_file\) =&gt; True is\_compound\('dogparrotcat', dictionary\_file\) =&gt; False
{% endhint %}

{% hint style="success" %}
1. Implement a function exists that indicates whether an argument passed in is part of the dictionary.
{% endhint %}

{% hint style="success" %}
Here's an example of a well thought out binary search solution:
{% endhint %}

{% code title="dict\_binary\_search.py" %}
```python
def get_word_at_pos(dict_file, pos):
    word = ''
    while pos > 0 and dict_file.read(1) != ' ':
        pos -= 1
        dict_file.seek(pos)
    cur = dict_file.read(1)
    while cur != ' ':
        word += cur
        cur = dict_file.read(1)
    return word, pos


def search(word, dict_file, begin, end):
    if begin == end:
        return False
    else:
        mid = (end+begin) / 2
        current_word, pos = get_word_at_pos(dict_file, mid)
        if word == current_word:
            return True
        else:
            mid = pos
            if word > current_word:
                next_begin = mid+len(current_word)+1
                if begin == next_begin:
                    return False
                else:
                    return search(word, dict_file, next_begin, end)
            else:
                next_end = mid
                if next_end == end:
                    return False
                else:
                    return search(word, dict_file, begin, mid)


def exists(word, filename):
    with open(filename, 'r') as dict_file:
        dict_file.seek(0, 2)
        begin = 0
        end = dict_file.tell()-1
        return search(word, dict_file, begin, end)

```
{% endcode %}



{% hint style="success" %}
2. If you could modify the format of this file to support more efficientlookups, what would you change about the file format?
{% endhint %}

{% hint style="success" %}
Some good answers:

* Instead of having variable length records, have fixed length records. This

  makes it easier to seek instead of having to search through the file.

* Store it as a binary lookup tree with fixed length records so that you can do

  easy lookups. For instance, instead of cat dog horse, you could have dog cat

  horse and determine where to binary jump next based on indicies \(see

  [http://en.wikipedia.org/wiki/Binary\_tree\#Arrays](http://en.wikipedia.org/wiki/Binary_tree#Arrays)\)

* Maintain a prefix tree at the beginning of the file that lets you determine

  if certain prefixes are part of the file, possibly with offsets that let you

  jump to the correct places. See also, SSTables.
{% endhint %}

{% hint style="info" %}
3. Compound words are words that are composed of other words. Using the exists\(\) function you implemented earlier, implement a function that indicates whether a word is a compound word.

Example solution:
{% endhint %}

```python
def is_compound(word, filename):
    if exists(word, filename):
        return True
    else:
        for i in xrange(len(word)):
            if exists(word[:i], filename):
                return is_compound(word[i:], filename)
            else:
                continue
        return False

```

