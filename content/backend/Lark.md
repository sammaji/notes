## Grammar
The grammar defines all the rules of your language and how to generate a parse tree.

Lark accepts grammar in [extended baccus naur form](https://www.wikiwand.com/en/Extended_Backus%E2%80%93Naur_form) or EBNF.

```bnf
rule_name:
	regex patterns to match or "string"
```

Example (for a json parser):

`()` -> grouping
`|` -> or
`[]` -> optional (zero or more occurrences)
`*` -> also means zero or more occurrences
`+` -> one or more instances

```
value: dict | list | STRING | NUMBER | "true" | "false" | "null"

list : "[" [value ("," value)*] "]"

dict : "{" [pair ("," pair)*] "}"

pair : STRING ":" value
```

We can also import rules, using `%import`. In the above example, we can import `STRING` and `NUMBER` from lark's common library.

```
// arrow (->) is used to rename a rule, ESCAPED_STRNG is renamed as STRING
%import common.ESCAPED_STRING -> STRING
%import common.SIGNED_NUMBER -> NUMBER
```

We also need to deal with white spaces and new-lines. In our case we can simply ignore it using `%ignore`

```lark
// import whitespaces
%import common.WS

// ignore it
%ignore WS
```

One more thing to note is that will generating syntax tree, lark will automatically ignore any unnamed string literal. Named literal are ignore if prefixed with underscore `_`.

Lark will not ignore any named or unnamed regex even unless prefixed with underscore `_`.

e.g., `"[" [value ("," value)*] "]"` -> here the brackets and commas are ignored in the syntax tree as they are unnamed string literals.

This would mean, lark would ignore `"true"` and `"false"` etc. We can fix that be doing this:

```
value: dict
	| list
	| STRING
	| NUMBER 
	| "true" -> true
	| "false" -> false
	| "null" -> null
```

We can use `?` to reduce a node if it has only one child. For example, if a node has only one child, it makes sense to just remove that node.

`Node value -> Node child` -> `Node child`

In our example, the value will have only one child. That means the value node is redundant.

`?value: ...`

```text
---- data
{"key": ["item0", "item1", 3.14]}

---- old syntax tree
value
  dict
    pair
      "key"
      value
        list
          value	"item0"
          value	"item1"
          value	3.14
          
---- reduced syntax tree
dict
  pair
    string	"key"
    list
      string	"item0"
      string	"item1"
      number	3.14
      true
```

## Generating the syntax tree

```python
## pip install lark
from lark import Lark

parser = Lark("contents of the .lark file")
text = '{ "name": "samyabrata maji", "socials": [{ "name": "github", "username": "samyabrata-maji" }, {"name": "twitter", "username": "sammaji15"}] }'

st = parser.parse(text)
print(st.pretty())
```