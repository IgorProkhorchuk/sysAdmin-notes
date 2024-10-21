Writing one-liner scripts in the command line is a common practice in Bash, allowing you to perform quick tasks without creating a full script file.

### 1. **Basic Structure of a One-Liner**
A Bash one-liner typically follows this structure:

```bash
command [arguments]; command2 [arguments]; command3 [arguments]
```

- **Commands are separated by semicolons (`;`)**.
- You can **chain multiple commands** together on a single line.
- **Redirection (`>`, `2>`, `>>`)** and **pipes (`|`)** are often used in one-liners to handle input/output.

### 2. **Examples of Common One-Liners**

#### a. Print "Hello, World!"
```bash
echo "Hello, World!"
```

#### b. Create and Write to a File
```bash
echo "This is a one-liner script" > file.txt
```

#### c. Combine Multiple Commands
- Create a file, list it, and delete it:
  ```bash
  touch file.txt; ls -l file.txt; rm file.txt
  ```

- Check if a file exists, if not, create it:
  ```bash
  [ ! -f file.txt ] && touch file.txt && echo "File created"
  ```

#### d. Loop One-Liner
- Print numbers from 1 to 5:
  ```bash
  for i in {1..5}; do echo $i; done
  ```

#### e. Conditional One-Liner
- If a directory exists, delete it; otherwise, create it:
  ```bash
  [ -d mydir ] && rm -r mydir || mkdir mydir
  ```

#### f. Find and Delete Files Older Than 7 Days
```bash
find /path/to/files -type f -mtime +7 -exec rm {} \;
```

#### g. Check Disk Space Usage
```bash
df -h | grep '/dev/sda1'
```

### 3. **Using Loops and Conditionals**

#### a. While Loop One-Liner
- Print numbers 1 to 5:
  ```bash
  i=1; while [ $i -le 5 ]; do echo $i; ((i++)); done
  ```

#### b. Conditional One-Liner
- Check if a file exists, and print a message if it does:
  ```bash
  [ -f file.txt ] && echo "File exists" || echo "File does not exist"
  ```

### 4. **Combining Commands with Pipes**

Pipes (`|`) allow you to pass the output of one command as input to another.

#### a. Count Lines in a File
```bash
cat file.txt | wc -l
```

#### b. Find a String in a File and Count Its Occurrences
```bash
grep "search_term" file.txt | wc -l
```

#### c. Show Running Processes and Filter by Name
```bash
ps aux | grep process_name
```

### 5. **Using Command Substitution**

Command substitution allows you to use the output of a command in another command by using `$()`.

#### a. Save the Current Date to a Variable
```bash
today=$(date); echo "Today is $today"
```

#### b. Create a File with a Timestamp
```bash
touch file_$(date +%Y-%m-%d).txt
```

### 6. **Redirecting Output in One-Liners**

#### a. Redirect stdout to a File
```bash
ls > filelist.txt
```

#### b. Redirect stderr to a File
```bash
ls non_existing_file 2> error_log.txt
```

#### c. Redirect Both stdout and stderr
```bash
command &> output.txt
```

### 7. **Background Execution**

Run a command in the background by adding `&` at the end.

#### a. Background Example
```bash
sleep 30 & echo "Sleeping in the background"
```

### 8. **Simple Function One-Liners**

You can define and use simple functions in one line as well.

#### a. Define a Function and Call It
```bash
greet() { echo "Hello, $1!"; }; greet "Alice"
```

### 9. **One-Liner with `awk`**

#### a. Print Specific Columns from a File
```bash
awk '{print $1, $3}' file.txt
```

### 10. **Chaining Commands with `&&` and `||`**

- **`&&`**: Executes the second command only if the first succeeds.
  - Example: Compile a program and run it if successful:
    ```bash
    gcc program.c -o program && ./program
    ```

- **`||`**: Executes the second command only if the first fails.
  - Example: Try to list a file, and print an error message if it fails:
    ```bash
    ls non_existing_file || echo "File not found"
    ```

### 11. **Escape Special Characters in One-Liners**

Use a backslash (`\`) to escape special characters or continue commands on the next line.

#### a. Continue a Command on the Next Line
```bash
echo "This is a long command" \
"and it's continued on the next line"
```

### 12. **Math Operations in One-Liners**

#### a. Perform Basic Arithmetic
- Calculate `5 + 3`:
  ```bash
  echo $((5 + 3))
  ```

- Store result in a variable:
  ```bash
  result=$((5 + 3)); echo $result
  ```

### 13. **Quickly Define Arrays**

#### a. Array Example in One-Liner
- Declare and print elements of an array:
  ```bash
  arr=(1 2 3 4 5); echo ${arr[@]}
  ```

---

