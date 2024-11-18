# Regular expressions (REGEX)


## Basic Syntax

| Pattern                | Description                               | Example                   |
|-----------------------|-------------------------------------------|---------------------------|
| `.`                   | Matches any single character except newline | `a.c` matches `abc`, `a-c` |
| `^`                   | Asserts position at the start of a line  | `^Hello` matches `Hello world` |
| `$`                   | Asserts position at the end of a line    | `world$` matches `Hello world` |
| `\`                   | Escapes a special character               | `\.` matches `.`            |

## Character Classes

| Pattern                | Description                               | Example                   |
|-----------------------|-------------------------------------------|---------------------------|
| `[abc]`               | Matches any single character within brackets | `[aeiou]` matches `a`, `e` |
| `[^abc]`             | Matches any character not in brackets     | `[^0-9]` matches `a`, `@`   |
| `[a-z]`              | Matches any lowercase letter              | `[a-z]` matches `x`        |
| `[A-Z]`              | Matches any uppercase letter              | `[A-Z]` matches `X`        |
| `[0-9]`              | Matches any digit                         | `[0-9]` matches `5`        |
| `[a-zA-Z]`           | Matches any letter                        | `[a-zA-Z]` matches `g`     |

## Predefined Character Classes

| Pattern                | Description                               | Example                   |
|-----------------------|-------------------------------------------|---------------------------|
| `\d`                  | Matches any digit (equivalent to `[0-9]`) | `\d{3}` matches `123`     |
| `\D`                  | Matches any non-digit character           | `\D` matches `a`          |
| `\s`                  | Matches any whitespace character          | `\s` matches ` `          |
| `\S`                  | Matches any non-whitespace character      | `\S` matches `a`          |
| `\w`                  | Matches any alphanumeric character        | `\w` matches `a`, `1`     |
| `\W`                  | Matches any non-alphanumeric character    | `\W` matches `!`          |

## Quantifiers

| Pattern                | Description                               | Example                   |
|-----------------------|-------------------------------------------|---------------------------|
| `*`                   | Matches 0 or more of the preceding element | `a*` matches `aa`, `a`, or `''` |
| `+`                   | Matches 1 or more of the preceding element | `a+` matches `aa` but not `''` |
| `?`                   | Matches 0 or 1 of the preceding element    | `a?` matches `a` or `''`  |
| `{n}`                 | Matches exactly `n` occurrences           | `a{3}` matches `aaa`      |
| `{n,}`                | Matches `n` or more occurrences           | `a{2,}` matches `aa`, `aaa`, `aaaa` |
| `{n,m}`               | Matches between `n` and `m` occurrences   | `a{1,3}` matches `a`, `aa`, `aaa` |

## Grouping and Alternation

| Pattern                | Description                               | Example                   |
|-----------------------|-------------------------------------------|---------------------------|
| `(...)`               | Groups multiple tokens together            | `(abc)+` matches `abc`, `abcabc` |
| `|`                   | Alternation (logical OR)                  | `cat|dog` matches `cat` or `dog` |

## Anchors

| Pattern                | Description                               | Example                   |
|-----------------------|-------------------------------------------|---------------------------|
| `\b`                  | Word boundary                             | `\bword\b` matches `word` but not `sword` |
| `\B`                  | Non-word boundary                         | `\Bword\B` matches `sword` |

## Assertions

| Pattern                | Description                               | Example                   |
|-----------------------|-------------------------------------------|---------------------------|
| `(?=...)`             | Positive lookahead                        | `\d(?= dollars)` matches `5` in `5 dollars` |
| `(?!...)`             | Negative lookahead                        | `\d(?! dollars)` matches `5` in `5 apples` |
| `(?<=...)`            | Positive lookbehind                       | `(?<=\$)\d+` matches `100` in `$100` |
| `(?<!...)`            | Negative lookbehind                       | `(?<!\$)\d+` matches `100` in `100 apples` |

## Flags

| Flag                  | Description                               |
|-----------------------|-------------------------------------------|
| `i`                   | Ignore case                               |
| `m`                   | Multiline (affects `^` and `$`)         |
| `s`                   | Dot matches newline                       |
| `x`                   | Ignore whitespace and comments            |

## Common Use Cases

### Email Validation

```regex
^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$
```

# Simple patterns

Most characters will match themselves exactly. You can enable/disable case sensitivity. Some special characters don't match themselves (meta characters) unless they signal that something out of the ordinary should happen (matching some text portion, repeating them, or changing their meaning).

## Metacharacters

The following are common meta characters in regex: **.  ^  $  *  +  ?  {  [  ]  \  |  (  )**

### Character Class `[ ]`

Used to specify a set of characters that should be matched. It can be an individual list or a range of characters (indicated by `-`), e.g., `[abcde]` or `[a-e]` will match any character from `a` to `e`.

**Note:** Meta-characters are not active inside classes.  
Example: `[akm$]` will match any of the characters `a`, `k`, `m`, or `$`.

You can complement the set of characters inside a class by using `^`, which matches all characters other than the listed.  
Example: `[^123]` will match any character other than `1`, `2`, and `3`.

Meta-characters can be used without their special properties by escaping them with a backslash (`\`). For example, `[` and `\` can be escaped like this: `\[` and `\\`.

## Predefined Special Sequences

- `\d` Matches any decimal digit (equivalent to class `[0-9]`).
- `\D` Matches any non-digit character (equivalent to class `[^0-9]`).
- `\s` Matches any whitespace character (equivalent to class `[ \t\n\r\f\v]`).
- `\S` Matches any non-whitespace character (equivalent to class `[^ \t\n\r\f\v]`).
- `\w` Matches any alphanumeric character (equivalent to class `[a-zA-Z0-9_]`).
- `\W` Matches any non-alphanumeric character (equivalent to class `[^a-zA-Z0-9_]`).
- `\A` Matches only at the start of the string. In MULTILINE mode, `\A` and `^` behave differently.
- `\Z` Matches only at the end of the string.
- `\b` Word boundary. Matches only at the beginning or end of a word.
- `\B` Matches when the current position is not at a word boundary.

These sequences can be included inside a character class.  
Example: `[\s,.]`

The final meta-character in this section is `.` which matches anything except the newline character. An alternative mode is `(re.DOTALL)`.

## Repeating things

The first meta-character for repeating things is `*`, which specifies that the previous character can be matched zero or more times.

**Example:**  
`ca*t` will match `ct`, `cat`, `caat`, `caaat`, and so on.

Another meta-character is `+`, which matches one or more times. Pay careful attention to the difference between `*` and `+`.  
**Example:**  
`ca+t` will match `cat`, `caat`, `caaaat`, but not `ct`.

The `?` meta-character matches either once or zero times, marking something as optional.  
**Example:**  
`meta-?character` can match either `metacharacter` or `meta-character`.  
`pass-?word` can match either `password` or `pass-word`.

The most complicated repeated qualifier is `{m,n}` where `m` and `n` are decimal integers. This qualifier specifies that there must be at least `m` repetitions and at most `n`.  
**Example:**  
`a/{1,3}b` will match `a/b`, `a//b`, `a///b` only. It won’t match `ab` or `a////b`.

If `m` or `n` are omitted, reasonable values are assumed. Omitting `m` assumes `0` as the lower limit, while omitting `n` results in an upper bound of infinity.  
- `{0,}` can represent `*`
- `{1,}` can represent `+`
- `{0,1}` can represent `?`

### Non-Greedy Filter

To make a match non-greedy, use `*?`, `+?`, `??`, or `{m,n}?`.  
**Example:**
```python
text = "<html><head><title>Title</title>"
print(re.match('<.*>', text).group())  # Returns the whole text due to greedy
print(re.match('<.*?>', text).group()) # Returns <html> which is non-greedy
```

## Alternation

The pattern `A|B` will match any string that matches either `A` or `B`.  
**Example:**  
`Crow|Servo` will match either `Crow` or `Servo`.  
To match the pipe character `|` itself, use `\|`.

## Anchors

- `^` matches the beginning of a line.
- `$` matches the end of a line.

## Groupings

Parentheses `()` are used to group strings together.  
**Example:**
```python
text = "<b> </b> the hell <b>is freezing</b>"
print(re.match(r'(<b>)*(</b>)'))  # Returns the first "<b> </b>"
```

## Word Boundary
To match a specific word, you can use the word boundary \b.
Example:
```python
p = re.compile(r'\bclass\b')
print(p.search('no class at all'))  # Returns object matching " class "
print(p.search('the declassified algorithm'))  # Doesn't return anything
```

### Compilation Flags
#### Flag	Description

I, IGNORECASE	Perform case-insensitive matching

L, LOCALE	Make \w, \W, \b, and \B depend on current locale (considering language differences)

M, MULTILINE	Allows ^ and $ to match the start and end of each line

### Using Regular Expressions
Example:
```python
text = "<b> </b><b>this </b> <b> \n \r </b> and that <b> \n\n\r</b>"
pattern = re.compile(r'(<b>)\s*(</b>)', re.IGNORECASE)
for a_match in pattern.finditer(text):
    print(a_match)                   # Returns a match object
    print(" ", a_match.group())      # Returns a matched string
    print(" ", a_match.span())       # Returns length of each string match
    print(" start:", a_match.start(), " end:", a_match.end())  # Returns start and end positions
```

### Replacing Subgroups
You can name subgroups using (?P<name>...) and refer to them with \g<name>.
Example:
```python
mystring = "my name\n is john francis ;\n mukulu you are \n welcome so\n ; much."
result = re.subn(r'(?P<first>[\w][\ ]*)[\n](?P<second>[\ ]*[\w])', r'\g<first> \g<second>', mystring)[0]
print(result)
# Returns: "my name is john francis ;\n mukulu you are welcome so\n ; much."
```


