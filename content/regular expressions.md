used for pattern matching.

- `abc` -> this regex will match "abc" in a string.
- `\d` or `\w` etc. -> they can be used to match special characters or sequences.
- `?`, `+` -> have special meaning, hence if you want to match "+", use a backslash before it, e.g. `\+`

- `[]` -> matches any one of the given options
- `[123]` will match either one or two or three.
- `[1-5]` -> will match any number from one to five.
- `[^abc]` -> inside square brackets `^` means negation. here, it matches any character other than a, b or c.
- `(a|b)` -> either a or b

- `.` -> match any character except newlines.
- `[^]` -> match any character.

NOTE: A lot of bugs in regular expression programs can be traced to unintentionally using a greedy operator where a nongreedy one would work better. When using a repetition operator, consider the nongreedy variant first.
- `*?`, `+?`, `{}?`  -> putting a "?" after these operators makes them nongreedy, meaning they will try to stop matching with as little as possible.
#### Boundaries
- `^` -> start of string or start of line if string is multi-line
- `\A` -> start of string
- `$` -> end of string, or end of line if string is multi-line
- `\Z` -> end of string

- `\b` -> word boundary
If you put `\b` before a word (alphanumeric) character, it will check if the character before it is non-alphanumeric. If you put it after a word, it will check if the character after the word is non-alphanumeric.

e.g., for the regex `\bcat` :
- `"The.catis happy"` will return a match, as the character before "cat" (`.`) is non-alphanumeric.
- `"Thecat is happy"` will return no match , as the character before "cat" (`e`) is alphanumeric.

If you wrap an non-alphanumeric pattern inside a word boundary, then it will check if alphanumeric characters exist before or after it or not.

e.g. for the regex `\.\b`:
- `"hello.world"` will return a match, as the character after `"."` (`w`) is alphanumeric.
- `"hello.,world"` will return no match, as the character after `"."` (`,`) is non-alphanumeric.

You can use a combination of alphanumeric and non-alphanumeric characters, it will only check for the word next to or before a word boundary.
e.g., `\bchello\.\b` -> think of this like `\bc` followed by `hello` followed by `\.\b`

- `\B` -> not word boundary
- `\<` -> start of word
- `\>` -> end of word
#### Quantifiers
- `+` -> can be repeated one or more times
- `*` -> can be repeated zero or more times
- `?` -> can be repeated zero or one times (at most one occurrence).
- `{3}` -> can occur precisely three times, e.g., `a{3}` or `[123]{3}`
- `{3,}` -> can occur three or more times
- `{3,5}` -> can occur three or four or five times, etc.

#### Character Classes
`.` -> any character except newline

Note, if a lowercase character represents a pattern, then its upper case will represent, anything but that pattern. e.g., `\w` means any alphanumeric character and `\W` means any non-alphanumeric character.

`\d` -> digit
`\w` -> alpha-numeric character
`\s` -> white space character (space, tab, newline)

### Common Regex Methods
regex.text(string) -> checks if there is a match in the given string.

regex.exec(string) -> returns an array-like with the first  occurrence of a matching pattern, followed by all the groups. it also has an `index` property indicating the start of the pattern in the string.

string.replace(x: pattern or string, y: string or function) -> x is the pattern or string you want to replace, y is the string you want to replace x with. y can be a function, in that case it returns a string.

NOTE: It is possible to refer to matched groups in the replacement string. e.g., `"hello world".replace(/(\w+) (\w+)/, "$2 $1)`, here $1 and $2 refers to the first and second groups. (output -> "world hello"). Use ` $&` refer to every group.
#### Regex Constructor
Dynamically create regex from strings using RegExp constructor.
`const reg = new RegExp("\\b")`

NOTE: use `\\` instead of single `\` for slashes
- `\w` -> `\\w`
- `\\` -> `\\\\`
---
string.search(pattern) -> returns the index of the first occurrence of given pattern.

### Matching and Grouping

### Exercise: Build a regex parser
