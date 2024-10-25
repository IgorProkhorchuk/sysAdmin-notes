The `sed` (stream editor) command is a powerful text-processing tool used for modifying files and streams in Unix/Linux. It operates by reading each line of a file or input, performing specified operations, and outputting the modified text.

### 1. **Basic Syntax**
The basic structure of the `sed` command is:

```bash
sed 'operation' filename
```

For example, if you want to replace the word "cat" with "dog" in `file.txt`:

```bash
sed 's/cat/dog/' file.txt
```

Here:
- `s` is the substitute command.
- `/cat/` is the search pattern.
- `/dog/` is the replacement string.

### 2. **Basic Substitute Command (`s`)**
The substitute command (`s`) is one of the most common uses of `sed`. Here's how to use it with various options:

#### Replace the First Occurrence in Each Line

```bash
sed 's/old_text/new_text/' filename
```

This replaces only the first occurrence of `old_text` with `new_text` on each line.

#### Replace All Occurrences in Each Line

```bash
sed 's/old_text/new_text/g' filename
```

Adding `g` (global) replaces **all** occurrences of `old_text` with `new_text` on each line.

#### Replace with Case Insensitivity

```bash
sed 's/old_text/new_text/Ig' filename
```

Adding `I` makes the search case-insensitive, so `old_text`, `Old_text`, and `OLD_TEXT` all match.

### 3. **Output to a New File**

By default, `sed` only outputs to the screen, not to the original file. To save changes, use `-i` to modify the file directly (or specify an output file using redirection):

```bash
sed -i 's/old_text/new_text/g' filename  # Overwrite file
sed 's/old_text/new_text/g' filename > newfile.txt  # Redirect to a new file
```

If you want to keep a backup of the original file, add an extension after `-i`, like `-i.bak`:

```bash
sed -i.bak 's/old_text/new_text/g' filename  # Creates filename.bak as a backup
```

### 4. **Using Regular Expressions**

`sed` supports regular expressions for more complex pattern matching:

- **Dot (`.`)**: Matches any single character.
  ```bash
  sed 's/.at/dog/' filename  # Replaces "cat", "bat", etc., with "dog"
  ```

- **Character Classes (`[]`)**: Matches any character inside brackets.
  ```bash
  sed 's/[cbr]at/dog/' filename  # Replaces "cat", "bat", or "rat" with "dog"
  ```

- **Start (`^`) and End (`$`) of Line**: Matches only at the start or end of a line.
  ```bash
  sed 's/^start/BEGIN/' filename  # Replaces "start" only if it's the first word on a line
  sed 's/end$/FINISH/' filename  # Replaces "end" only if it's the last word on a line
  ```

### 5. **Multiple Commands with `-e`**

You can chain multiple `sed` commands together using `-e`:

```bash
sed -e 's/old/new/' -e 's/foo/bar/' filename
```

Or use curly braces `{}` to apply multiple commands to specific lines:

```bash
sed '2,5{s/foo/bar/; s/hello/world/}' filename  # Runs two replacements on lines 2-5
```

### 6. **Deleting Lines**

The `d` command is used to delete lines:

- **Delete Lines by Pattern**
  ```bash
  sed '/unwanted_text/d' filename  # Deletes lines containing "unwanted_text"
  ```

- **Delete Specific Line Numbers**
  ```bash
  sed '2d' filename  # Deletes the second line
  sed '2,5d' filename  # Deletes lines 2 through 5
  ```

### 7. **Inserting and Appending Text**

To insert or append text around specific patterns, use `i` (insert) and `a` (append):

- **Insert Text Before a Pattern**
  ```bash
  sed '/pattern/i\Text to insert' filename
  ```

- **Append Text After a Pattern**
  ```bash
  sed '/pattern/a\Text to append' filename
  ```

### 8. **Replacing Text with Line Variables**

When replacing text, `&` represents the matched text. Here’s how to use it:

```bash
sed 's/unix/& and linux/' filename  # Replaces "unix" with "unix and linux"
```

### 9. **Advanced Example: Replacing and Modifying Files in Place**

Suppose you have a file with names, and you want to add a prefix and suffix:

```bash
# original.txt
Alice
Bob
Charlie
```

Using `sed`:

```bash
sed 's/^/Mr. /; s/$/, PhD/' original.txt
```

**Output:**
```
Mr. Alice, PhD
Mr. Bob, PhD
Mr. Charlie, PhD
```

### 10. **Escape Characters in `sed`**

Since `sed` uses `/` as a delimiter, it can be confusing if your pattern or replacement contains `/`. In such cases, use an alternative delimiter, like `#`:

```bash
sed 's#path/to/old#path/to/new#g' filename
```

### Summary

Here's a quick overview of `sed` commands:

| Command | Description |
|---------|-------------|
| `s/pattern/replacement/` | Substitute pattern with replacement |
| `g` | Global replacement (all occurrences) |
| `i` | Insert text before a match |
| `a` | Append text after a match |
| `d` | Delete lines |
| `-i` | Edit file in place |

---
Absolutely! `sed` offers a variety of additional features, such as complex pattern matching, advanced line range selection, grouping with parentheses, and buffers. Let's dive into some powerful `sed` features.

### 1. **Range Patterns**

`sed` allows you to specify line ranges to perform operations only on certain lines.

#### Select a Range by Line Number
To apply commands only to a specific range of lines (e.g., lines 3 to 6):

```bash
sed '3,6s/foo/bar/' filename
```

This replaces occurrences of "foo" with "bar" only on lines 3 through 6.

#### Range by Patterns
You can also specify a range based on matching patterns.

```bash
sed '/start_pattern/,/end_pattern/s/foo/bar/' filename
```

This replaces "foo" with "bar" on lines between `start_pattern` and `end_pattern` (inclusive).

### 2. **Using `&` to Refer to the Matched Text**

The `&` symbol can be used to reference the whole matched string within the replacement section.

```bash
sed 's/[a-zA-Z]*/(&)/' filename
```

This wraps each word in parentheses. For example, "hello world" becomes "(hello) (world)".

### 3. **Using Grouping with Parentheses and Backreferences**

Parentheses allow grouping, and backreferences (`\1`, `\2`, etc.) let you refer to these groups in replacements.

```bash
sed 's/\([a-zA-Z]*\) \([a-zA-Z]*\)/\2 \1/' filename
```

This swaps the first and second words on each line. For example, "John Doe" becomes "Doe John".

### 4. **Conditional Execution with `;` or `-e`**

To chain multiple `sed` commands conditionally, use `;` within a single command or `-e`:

```bash
sed '/pattern1/s/foo/bar/; /pattern2/s/bar/foo/' filename
```

This will substitute "foo" with "bar" if "pattern1" is matched on the line, and swap "bar" back to "foo" if "pattern2" matches.

### 5. **Hold and Pattern Buffers**

`sed` maintains two buffers for text manipulation: the **pattern space** (current line being processed) and the **hold space** (an auxiliary storage area). Commands like `h`, `H`, `g`, `G`, `x` control data flow between these buffers.

#### Copying Lines with `h`, `H`, `g`, `G`, and `x`

- **`h`**: Copy pattern space to hold space.
- **`H`**: Append pattern space to hold space.
- **`g`**: Replace pattern space with hold space.
- **`G`**: Append hold space to pattern space.
- **`x`**: Swap pattern and hold spaces.

**Example: Swapping Two Lines**

```bash
sed 'N; s/\(.*\)\n\(.*\)/\2\n\1/' filename
```

- `N`: Pulls in the next line into the pattern space.
- `s/\(.*\)\n\(.*\)/\2\n\1/`: Reorders the two lines by grouping them with `\(.*\)` and referencing them as `\1` and `\2`.

### 6. **Inserting Text at Line Boundaries**

You can insert text at the start or end of files using `sed`.

#### Insert at the Start of File

```bash
sed '1i\This is the start of the file' filename
```

The `1i\` command inserts the specified text on the first line.

#### Insert at the End of File

```bash
sed '$a\This is the end of the file' filename
```

The `$a\` command appends text at the last line.

### 7. **Deleting Based on Complex Patterns**

You can remove lines that match certain patterns or based on other conditions.

#### Delete Empty Lines

```bash
sed '/^$/d' filename
```

This deletes lines that are empty (`^$` matches lines with no characters).

#### Delete Lines Based on Multiple Patterns

To delete lines containing either "error" or "fail":

```bash
sed '/error\|fail/d' filename
```

The `\|` symbol matches either "error" or "fail" on a line.

### 8. **Advanced Substitution Using `e` for Command Execution**

With the `e` flag, `sed` can execute a command from within the substitution. This works in some versions of `sed` and can be very powerful.

```bash
echo "Current directory: " | sed 's/$/$(pwd)/e'
```

This appends the output of `pwd` to the line.

### 9. **Recursive and In-place Editing**

You can use `sed` in scripts for bulk file changes across directories.

#### Recursively Find and Replace

To replace text in multiple files, combine `find` with `sed`:

```bash
find /path/to/dir -type f -name "*.txt" -exec sed -i 's/foo/bar/g' {} \;
```

This finds all `.txt` files under a directory and replaces "foo" with "bar" in place.

### 10. **Using Sed in a Script for Batch Processing**

Here's a script example that uses multiple `sed` commands to standardize text formatting:

```bash
#!/bin/bash

# Standardize text in all .txt files
for file in *.txt; do
  sed -i '
    s/old_word/new_word/g      # Replace words
    /^#/d                      # Delete comment lines
    s/\b[0-9]\{4\}\b/****/g    # Mask 4-digit numbers
    ' "$file"
done
```

### Summary of Additional `sed` Commands

| Command | Description |
|---------|-------------|
| `N` | Pulls in the next line into the pattern space |
| `h`, `H` | Copy or append pattern space to hold space |
| `g`, `G` | Replace or append hold space to pattern space |
| `x` | Swap pattern and hold spaces |
| `e` | Execute a shell command within the substitution |
| `1i`, `$a` | Insert text at the start or end of the file |

---

