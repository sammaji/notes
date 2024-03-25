### move one character
h -> left
j -> top
k -> bottom
l -> right

```
   j             -- up
h     l          -- left right
   k             -- down
```

### move one word

w -> right
> e.g., <u>f</u>unction hello() -> function <u>h</u>ello()

w -> beginning of next word
b -> beginning of previous word

e -> end of next word
ge -> end of previous word

**what is a word in vim?**
-> any sequence of letters, numbers or digits OR any sequence of special non-blank characters.
-> e.g. "hello", "(((", etc.
-> e.g. "hello()" - 2 words.

NOTE: vim has two different types of words -> 1. word and 2. WORD

WORD in vim includes some special characters too.
```
hello_world(){}
---
words: hello_world, (){}
WORDS: hello_world(){}
```

To navigate WORDS, we use capital letters, W, E, GE.

### find a character
f{character} -> jumps to the next occurrence of the character in the line
F{character} ->  jumps to the previous occurrence of the character in the line

e.g. fa -> next occurrence of a.

```
F (< left)    f (right >)   -- move to next occurence
```

t{ch} / T{ch} -> does the same thing but puts the cursor before the character.

```
                  v
fa -->  function cat() {} -- cursor at character 

                 v  
ta -->  function cat() {} -- cursor before character
```

*mnemonic*: f is find and t is un<u>t</u>il.

summary:
1.  f {ch} -> next occ of charecter
2. ; -> move to the next occ of the same character
3. , -> move to the prev occ of the same character

e.g. `fd;;` will do the same thing as `fdfdfd`