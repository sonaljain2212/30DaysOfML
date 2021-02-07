#30daysoftechreading

Day 13/30

Quote of the day: re.compile("Hey!! you are doing great!! Keep it up." )

Ever thought of doing a cool project trying your hands on text mining but stuck at where to start? How to get the important information from the gazillion strings of data? I would suggest starting with regex here. Read this very simple yet very comprehensive article “A simple intro to Regex with Python”. 

Link: (https://towardsdatascience.com/a-simple-intro-to-regex-with-python-14d23a34d170) 

Regular expressions are used to identify whether a pattern exists in a given sequence of characters (string) or not and also to locate the position of the pattern in a corpus of text.They help in manipulating textual data, which is often a pre-requisite for data science projects that involve text analytics.

In Python, there is a built-in module called re, which needs to be imported for working with Regex.

```
import re
```

The official documentation page (https://docs.python.org/3/howto/regex.html)

You can look at the examples in the article and the official documentation for a good understanding.

## Methods

### - 1. The ‘match’ method:

We use thematch method to check if a pattern matches a string/sequence. It is case-sensitive.

```
p = re.compile('(ab)*')
print(p.match('ababababab').span())
```

### - 2. A `compile`d program

Instead of repeating the code, we can use compile to create a regex program and use built-in methods.

```
 p = re.compile('ab*')
```
### - 3. Positional matching

We can easily use additional parameters in the match object to check for positional matching of a string pattern.

```
p = re.compile('(ab)*')
print(p.match('ababababab' , pos =1 ).span())
```

### - 4. The `findall` and `finditer` methods

The search is powerful but it is also limited to finding the first occurring match in the text. To discover all the matches in a long text, we can use findall and finditer methods.

The findall method returns a list with the matching pattern. You can count the number of items to understand the frequency of the searched term in the text.
The finditer method produces an iterator. We can use this to see more information, as shown below.

```
p = re.compile(r'\d+')
>>> p.findall('12 drummers drumming, 11 pipers piping, 10 lords a-leaping')
['12', '11', '10']
```

```
>>> iterator = p.finditer('12 drummers drumming, 11 ... 10 ...')
>>> iterator  
<callable_iterator object at 0x...>
>>> for match in iterator:
...     print(match.span())
...
(0, 2)
(22, 24)
(29, 31)
```

### - 5. Wildcard matching (with single characters)

Now, we gently enter the arena where Regex shines through. The most common use of Regex is related to ‘wildcard matching’ or ‘fuzzy matching’. This is where you don’t have the full pattern but a portion of it and you still want to find where in a given text, something similar appears.
Here are various examples. Here we will also apply thegroup() method on the object returned by search to essentially return the matched string.

  - Single-character matching by DOT: 

    Dot(.) matches any single character except the newline character.

  - Lowercase \w to match any single letter, digit or underscore: 
    DOT is limited to alphabetical characters, so we need to expand the repertoire with other tools. Dot(.) matches any single character except the newline character.

  - (\W or uppercase W) matches anything not covered with \w:
    There are symbols other than letter, digits, and underscore. We use \W to catch them.

  - Matching patterns with whitespace characters:
    \s (lowercase s) matches a single whitespace character like space, newline, tab, return. Naturally, this is used to search for a pattern with whitespace inside it e.g. a pair of words.


  - Start of a string:
    The ^(caret) matches pattern at the beginning of a string (but not anywhere else).


  - End of a string:
    The $ (dollar sign) matches a pattern at the end of the string. Following is a practical example where we are only interested in pulling out the patent information of Apple and discard other companies. We check the end of the text for ‘Apple’ and only if it matches, we pull out the patent number using the numerical digit matching code we showed earlier.


### - 6. Wildcard matching (with multiple characters)
Now, we can move on to more complex wildcard matching with multiple characters, which allows us much more power and flexibility.

  - Matching 0 or more repetitions: * matches 0 or more repetitions of the preceding regular expression.

  - Matching 1 or more repetitions: + causes the resulting RE to match 1 or more repetitions of the preceding RE.


  - Matching precisely 0 or 1 repetition: ? causes the resulting RE to match precisely 0 or 1 repetitions of the preceding RE.

  - Controlling how many repetitions to match: {m} specifies exactly m copies of RE to match. Fewer matches cause a non-match and returns None.

  - Sets of matching characters: [x,y,z] matches x, y, or z.

  - Range of characters inside a set: A range of characters can be matched inside the set. This is one of the most widely used regex techniques. We denote range by using a -. For example, a-z or A-Z will match anything between a and z or A and Z i.e. the entire English alphabet.
Let’s suppose, we want to extract an email id. We put in a pattern matching regex with alphabetical characters + @ + .com. But it cannot catch an email id with some numerical digits in it.

### - 7. The Split method
Finally, we talk about a method that can be used in creative ways to extract meaningful text from an irregular corpus. A simple example is shown below, where we build a Regex pattern with the extrinsic characters which are messing up a regular sentence and use the split() method to get rid of those characters from the sentence.
