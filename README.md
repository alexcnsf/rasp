** Prerequisites **

In order to interact with rasp enviroment you must first initailize it with the command:

```
$ ./setup.sh
```

And then start the interactive enviroment using the command
```
$ ./rasp.sh
```

You will be prompted ``` >> ``` where you can define functions or run them!

**Problem 1:**
Write an s-op that contains the indices in reverse order.
For example:
```
> reverse_indices("hello")
[4, 3, 2, 1, 0]
```

Solution:


```
>> reverse_indices = length - indices - 1;
     s-op: reverse_indices
 	 Example: reverse_indices("hello") = [4, 3, 2, 1, 0] (ints)
```

Output:
```
>> reverse_indices("hello");
         =  [4, 3, 2, 1, 0] (ints)
```


**Problem 2:**
Write a function that "rotates" the input text by the specified number of characters.
For example:
```
> rotate(tokens, 0)("hello")
"hello"
> rotate(tokens, 1)("hello")
"ohell"
> rotate(tokens, 2)("hello")
"lohel"
```

Solution:
```
>> def rotate(seq, amount) {
..       new_indices = (indices + amount) % length; 
..       return aggregate(select(new_indices, indices, ==), seq); 
..   }
     console function: rotate(seq, amount)
```

Output:
```
>> rotate(tokens, 0)("hello");
         =  [h, e, l, l, o] (strings)
>> rotate(tokens, 1)("hello");
         =  [o, h, e, l, l] (strings)
>> rotate(tokens, 2)("hello");
         =  [l, o, h, e, l] (strings)
```

**Problem 3:**
Write a function that takes a sequence as input and "swaps every letter with its neighbor".
Specifically, for every even index $i$, positions $i$ and $i+1$ will be swapped;
if the length of the sequence is odd, then the last element should not move.
For example:
```
> swap(tokens)("hello")
"ehllo"
> swap(tokens)("ababab")
"bababa"
```

Solution:
```
def swap(seq) {
  return aggregate(select(indices, indices+1, ==), seq, "x") 
    if indices % 2 == 0 
    else aggregate(select(indices, indices-1, ==), seq, "x");
}
```

Output:
```
>> swap(tokens)("ababab");
         =  [b, a, b, a, b, a] (strings)
>> swap(tokens)("hello");
         =  [e, h, l, l, o] (strings)
```


**Problem 4:**
Write a function that returns the maximum value in the sequence repeated for every position.
For example:
```
> maxseq(tokens)("ababcabab")
"ccccccccc"
```

Solution:
```
>> def maxseq(seq) {
     return load_from_location(sorted, lastone);
     }
     console function: maxseq(seq)
```

Output:
```
>> sorted = sort(tokens, tokens);
     s-op: sorted
         Example: sorted("ababcabab") = [a, a, a, a, b, b, b, b, c] (strings)
```


**Problem 6:**
Write a function that counts the number of times a certain token appears in the input sequence.
For example:
```
> howmany(tokens, "a")("hello")
"00000"
> howmany(tokens, "h")("hello")
"11111"
> howmany(tokens, "l")("hello")
"22222"
```

Solution:
```
def howmany(seq, atom){
  return selector_width(select(seq, atom, ==)) if contains(seq, atom) else "0";
  }
```

Output:
```
howmany(tokens, "a")("hello");
         =  [0]*5 (strings)
howmany(tokens, "h")("hello");
         =  [1]*5 (ints)
howmany(tokens, "l")("hello");
         =  [2]*5 (ints)
```


**Problem 7:**
Write a function that counts the number of times a certain token has appeared in the input sequence so far.
For example:
```
> howmany(tokens, "a")("hello")
"00000"
> howmany(tokens, "h")("hello")
"11111"
> howmany(tokens, "e")("hello")
"01111"
> howmany(tokens, "l")("hello")
"00122"
```

Solution:
```
def howmany(seq,atom){
   return round(
   length*aggregate(
   full_s,indicator(seq==atom)));
   }
```

Output:
```
>> howmany(tokens, "a")("hello");
         =  [0]*5 (ints)
```

**Problem 8:**
Create your own "interesting" problem statement.
Write a function/s-op that solves this problem.

Write a function that returns the frequency of each token in the input sequence.

Solution:
```
>> token_counts = selector_width(select(tokens, tokens, ==));
     s-op: token_counts
 	 Example: token_counts("hello") = [1, 1, 2, 2, 1] (ints)
>> token_density = token_counts / length;
     s-op: token_density
 	 Example: token_density("hello") = [0.2, 0.2, 0.4, 0.4, 0.2] (floats)
```

Output:
```
>> token_density("hello");
	 =  [0.2, 0.2, 0.4, 0.4, 0.2] (floats)
```
