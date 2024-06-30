---
title: awk
tags:
  - linux
  - linux-commands
  - awk
draft: false
---
*it's often said that `awk` is a programming language.*

See [GNU Awk Documentation](https://www.gnu.org/software/gawk/manual/gawk.html)

`awk` scans over a text file, it treats each line individually and in succession, like an array. each line is a record.

each record is broken into fields.

`NR` -> no of. records
`NF` -> no of. fields

to print no of lines in a file, run:
```awk
awk 'END { print NR; }' sample.txt
```

### structure of `awk` script
`awk` script have a pattern or keyword, and an action it performs when the keyword is encountered.
```
pattern or keyword { action }
```

in the previous script, we used `END`, which only executes at the end of the parsing data.

you can use a pattern instead, to filter results. here `$0` will store the current `record`, i.e., the line in which a match is found.

```
awk '/Linux/ { print $0; }' sample.txt
```

`$0` -> current record
`$1` -> current field (in our example, it's "Linux")
`$2` -> next field (word next to "Linux"), and so on...

### field separator
by default, fields are separated by spaces, but you can change that by using the `-F` flag. it sets the `FS` variable.

> run `man awk | awk '/(f|F)ield.*separator/ {print NR "|" $0;}'` to search man documentation on field separator.

```
awk -F ':' [...]
```

### functions
here's the function semantics in awk.
```
name(parameters) { action }
```

there are functions to perform mathematical operations and string processing.

math ones are often fairly straightforward. you provide a number, and it crunches it.
```
awk 'BEGIN { print sqrt(1764); }'
---
42
```

