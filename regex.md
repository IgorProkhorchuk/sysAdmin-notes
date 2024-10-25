Regular expressions (regex) are patterns used to match character combinations in text. They are powerful tools for searching, extracting, and manipulating strings based on complex patterns. Regex is widely used across programming languages and command-line tools (like `sed`, `awk`, and `grep`), making it valuable to understand well.


---

### 1. **Basics of Regex Syntax**

#### Literal Characters
- **Basic Match**: If you enter a character without any special syntax, regex will try to match that exact character in the text.
  - **Example**: `cat` matches "cat" in "cat is here" but not "Cat" (since regex is case-sensitive by default).

#### Special Characters (Metacharacters)
These characters have special meanings in regex and include: `^`, `$`, `.`, `*`, `+`, `?`, `{}`, `[]`, `()`, `|`, `\`.

| Character | Meaning |
|-----------|---------|
| `.`       | Matches any single character except newline |
| `^`       | Matches the start of a line |
| `$`       | Matches the end of a line |
| `*`       | Matches 0 or more of the preceding character |
| `+`       | Matches 1 or more of the preceding character |
| `?`       | Matches 0 or 1 of the preceding character |
| `{}`      | Specifies the exact number of occurrences |
| `[]`      | Matches any character in the set (character class) |
| `()`      | Groups patterns and captures them for backreference |
| `|`       | Acts as an OR operator |
| `\`       | Escapes a metacharacter to match it literally |

### 2. **Anchors**

Anchors do not match actual characters but rather positions within a string.

- **Start of Line (`^`)**: Matches at the beginning of a line.
  - **Example**: `^cat` matches "cat" at the start of a line.
- **End of Line (`$`)**: Matches at the end of a line.
  - **Example**: `cat$` matches "cat" at the end of a line.
- **Word Boundary (`\b`)**: Matches positions at the boundaries of words.
  - **Example**: `\bcat\b` matches "cat" as a whole word, not as part of "catalog".

### 3. **Quantifiers**

Quantifiers specify the number of occurrences to match.

| Quantifier | Meaning |
|------------|---------|
| `*`        | Matches 0 or more occurrences of the preceding element |
| `+`        | Matches 1 or more occurrences of the preceding element |
| `?`        | Matches 0 or 1 occurrence of the preceding element |
| `{n}`      | Matches exactly `n` occurrences |
| `{n,}`     | Matches `n` or more occurrences |
| `{n,m}`    | Matches between `n` and `m` occurrences |

**Examples**:
- `a*` matches `""`, `a`, `aa`, `aaa`, etc.
- `a+` matches `a`, `aa`, `aaa`, etc., but not `""`.
- `a{3}` matches exactly `aaa`.
- `a{2,4}` matches `aa`, `aaa`, or `aaaa`.

### 4. **Character Classes**

Character classes allow you to specify a set of characters to match.

- **Basic Character Class (`[abc]`)**: Matches any one of the characters inside the brackets.
  - **Example**: `[aeiou]` matches any vowel.
- **Range (`[a-z]`)**: Matches any character within the specified range.
  - **Example**: `[A-Z]` matches any uppercase letter.
- **Negated Character Class (`[^abc]`)**: Matches any character not inside the brackets.
  - **Example**: `[^0-9]` matches any non-digit character.

#### Common Shorthand Character Classes
| Shorthand | Meaning |
|-----------|---------|
| `\d`      | Matches any digit (equivalent to `[0-9]`) |
| `\D`      | Matches any non-digit |
| `\w`      | Matches any word character (alphanumeric + underscore) |
| `\W`      | Matches any non-word character |
| `\s`      | Matches any whitespace character (spaces, tabs, newlines) |
| `\S`      | Matches any non-whitespace character |

### 5. **Grouping and Capturing**

Parentheses `()` are used to group patterns together and create capturing groups.

#### Grouping
Grouping allows us to apply quantifiers to entire patterns rather than just single characters.

- **Example**: `(ab)+` matches "ab", "abab", "ababab", etc.

#### Capturing
When groups are matched, they are saved and can be referenced later using backreferences (`\1`, `\2`, etc.).

- **Example**: In `(cat) and \1`, if `cat` is matched, `\1` refers back to that match.

#### Non-Capturing Groups
If you want to group without capturing, use `(?: ...)`.

- **Example**: `(?:cat|dog)` matches "cat" or "dog" but does not capture it for backreferencing.

### 6. **Alternation (`|`)**

The `|` operator provides a choice between patterns, acting as a logical OR.

- **Example**: `cat|dog` matches either "cat" or "dog".

### 7. **Lookahead and Lookbehind (Advanced)**

Lookahead and lookbehind are special types of assertions that allow you to match based on what comes before or after a certain pattern.

#### Positive Lookahead (`?=`)

Matches a pattern only if it is followed by another pattern.

- **Example**: `cat(?=dog)` matches "cat" only if it is followed by "dog".

#### Negative Lookahead (`?!`)

Matches a pattern only if it is *not* followed by another pattern.

- **Example**: `cat(?!dog)` matches "cat" only if it is not followed by "dog".

#### Positive Lookbehind (`?<=`)

Matches a pattern only if it is preceded by another pattern.

- **Example**: `(?<=dog)cat` matches "cat" only if it is preceded by "dog".

#### Negative Lookbehind (`?<!`)

Matches a pattern only if it is *not* preceded by another pattern.

- **Example**: `(?<!dog)cat` matches "cat" only if it is not preceded by "dog".

### 8. **Putting It All Together: Complex Examples**

#### Example 1: Email Validation
A regex to match valid email formats:

```regex
^[\w\.-]+@[a-zA-Z\d\.-]+\.[a-zA-Z]{2,6}$
```

#### Example 2: Extracting Date Components (MM-DD-YYYY)
To extract month, day, and year from a date like "12-25-2024":

```regex
(\d{2})-(\d{2})-(\d{4})
```

- `\1`, `\2`, and `\3` will contain the month, day, and year, respectively.

---

