### input

#### single char input
`getchars` -> takes a single character input
#### scanf function
- `%s` -> string
- `%5s` -> read only 5 characters
- `%[pattern]` -> matches pattern
	- e.g, `%[^\n]` -> matches everything other than new-lines
- `%d` -> integers
- `%f` -> float
- `%lf` -> double

## conditionals
switch case syntax
```c
switch (condition) {
	case a:
		block;
		break;
	case b:
	case c:
		block;
		break;
	default:
		block;
}
```

