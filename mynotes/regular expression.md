# regular expression

## patterns and flags

1. create a regular expression object

	- regexp = new RegExp("pattern", "flags");
	- regexp = /pattern/flags;

2. flags

	- i : case-insensitive
	- g : search for all matches
	- m : multiline mode
	- u : enable full unicode support
	- y : sticky mode

## methods of RegExp and String

### regular expression's methods

	`res = regexp.method(str)` *method* here is test, exec ...

1. **test** : search the string and return true/false

2. **exec** : 
	- no 'g' flag : res[0], res[1], ..., res.index, res.input (exactly as str.match())
	- has 'g' flag : res[0], res[1], ..., res.index, res.input (the regexp has lastIndex property, can search continuously until null)
	- has 'y' flag : only search at the specified position

### regular string work with regexps

	`res = str.method()` *method* here is search, match ...

1. **search** : only looks for the first position

2. **match** : 
	- no 'g' flag : res[0], res[1], ..., res.index, res.input (result include capture groups and 2 additional properties)
	- has 'g' flag : res[0], res[1], ... (result is a simple array of matches)
	- **note** : if there are no matches, the call to match returns null, not [].

3. **split** : str.split(regexp|substr, limit), use regexp or substring as a delimiter

4. **replace** : str.replace(str1|reg, str2|func) , swiss army knife for search and replace
	- use special characters in str2: `$$`: $, `$&`: the whole match, `$n`: n-th parentheses, ``$` ``: before match, `$'`: after match
	- use func relieaze smart replacement: `func(str, p1, p2, ..., pn, offset, s)`

## character classes

- \d – digits.
- \D – non-digits.
- \s – space symbols, tabs, newlines.
- \S – all but \s.
- \w – English letters, digits, underscore '_'.
- \W – all but \w.
- \b - word boundary, 'zero width' in a sense
- \B - non-boundary
- '.' – any character except a newline.
- spaces are regular characters

## Escaping, special characters

- Special characters: `[ \ ^ $ . | ? * + ( )`
- Open and close symboll: slash `/`

To use these characters as a regular one, prepend it with a backslash.
That’s also called “escaping a character”.

**new RegExp** : The quotes “consume” and interpret them
	
- \n – becomes a newline character,
- \u1234 – becomes the Unicode character with such code,
- …And when there’s no special meaning: like \d or \z, then the backslash is simply removed.
	
`new RegExp("\d\.\d") = /d.d/`
`new RegExp("\\d\\.\\d") = /\d\.\d/`

## Sets and ranges

1. Sets : [abc] one character a or b or c
2. Ranges : 
	- `\d = [0-9]`
	- `\w = [a-zA-Z0-9_]`
	- `\s = [\t\n\v\f\r]`
	- `[\s\S]` any character , while `.` except a newline
3. Excluding ranges : 
	`[^\d\sA-Z]` – any character except '\d', '\s', or 'A-Z'
4. `. + ( ) - ^ [` can use without escaping symbol '\' in square brackets

## Quantifiers

- `{m,n}`
- `+` : one or more , {1,}
- `?` : zero or more , {0,1}
- `*` : zero or more, {0,}

### greedy mode (default)

Greediness is the cause of all evil

`'a "witch" and her "broom" is one'.match(/".+"/g) = "witch" and her "broom"`

quantifier is repeated as many times as possible;

regex engine tries to fetch as many characters as it can, then shortens that one by one.

### lazy mode with symbol ?

`+?` `??` `*?`
regex engine increases the number of repetitions only the rest can't match

`/"[^"]+"/g` sometimes performs better than `/".+?"/g`

## Capturing groups

1. It allows to place a part of the match into a separate array item when using `String#match` or `RegExp#exec` methods.
2. If we put a quantifier after the parentheses, it applies to the parentheses as a whole, not the last character.
3. `(?:go)+` the 'go' is treated as a whole, but not a capture group

## Backreferences: \n and $n

1. `\n` in string method:  `"John Smith".replace(/(\w+) (\w+)/i, "$2, $1")`
2. `$n` in pattern: 
```
	let str = "He said: \"She's the one!\".";
	let reg = /(['"])(.*?)\1/g;
	alert( str.match(reg) ); // "She's the one!"
```

## Alternation (OR) |

- The caret ^ matches at the beginning of the text
- the dollar $ – in the end.

## Multiline mode: flaf "m"

1. only affect the behavior of `^` and `$`: line begin and end
2. `/\w+\n/gim` newline character '\n' 



