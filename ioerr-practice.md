### Task 1: Redirecting stdout to a file
Run the `ls` command and redirect its output to a file named `file_list.txt`. Verify the contents of the file.
```bash
# Command to run:
ls > file_list.txt
# Verify the output:
cat file_list.txt
```

### Task 2: Redirecting stderr to a file
Try to list a non-existent file and redirect the error message to a file called `errors.txt`. Ensure the terminal shows no output, and then view the contents of `errors.txt`.
```bash
# Command to run:
ls non_existent_file 2> errors.txt
# Verify the output:
cat errors.txt
```

### Task 3: Redirecting both stdout and stderr
Run a command that produces both output and errors (like `ls` on a directory with a mix of files and non-existent entries). Redirect both stdout and stderr to a single file named `combined_output.txt`.
```bash
# Command to run:
ls file_that_exists non_existent_file > combined_output.txt 2>&1
# Verify the output:
cat combined_output.txt
```

### Task 4: Appending stdout to a file
Use the `echo` command to append the text "Hello, World!" to a file named `greetings.txt`. Run the command multiple times and check that each time the new text is added without overwriting the previous content.
```bash
# Command to run:
echo "Hello, World!" >> greetings.txt
# Verify the output:
cat greetings.txt
```

### Task 5: Redirecting stdin from a file
Create a file named `input.txt` with some text (you can use any text editor). Then, use the `cat` command to read from the file by redirecting `stdin` and display the contents on the terminal.
```bash
# Command to run:
cat < input.txt
```

### Task 6: Using pipes to filter output
Use the `ls` command to list files in the `/usr/bin` directory. Then, use a pipe (`|`) to pass the output of `ls` to the `grep` command to search for files that contain the word "python".
```bash
# Command to run:
ls /usr/bin | grep python
```

### Task 7: Redirecting stderr while keeping stdout
Run a command that produces both regular output and errors. Redirect only the error messages (stderr) to a file called `errors_only.txt` while allowing the regular output to appear on the terminal.
```bash
# Command to run:
ls file_that_exists non_existent_file 2> errors_only.txt
# Verify the output:
cat errors_only.txt
```

### Task 8: Redirecting both stdout and stderr to separate files
Run a command that generates both stdout and stderr. Redirect stdout to a file named `output.txt` and stderr to a file named `errors.txt`.
```bash
# Command to run:
ls file_that_exists non_existent_file > output.txt 2> errors.txt
# Verify the output:
cat output.txt
cat errors.txt
```

### Task 9: Using pipes with multiple commands
Use the `ps aux` command to list running processes. Pipe the output through `grep` to find all processes related to `bash`. Then, use `wc -l` to count how many `bash` processes are running.
```bash
# Command to run:
ps aux | grep bash | wc -l
```

### Task 10: Combining redirection and pipes
Create a file `data.txt` with the following contents:
```
apple
banana
orange
grape
```
Use the `cat` command to display the contents of `data.txt`, then pipe the output to the `sort` command to sort the lines alphabetically. Redirect the sorted output to a new file `sorted_data.txt`.
```bash
# Command to run:
cat data.txt | sort > sorted_data.txt
# Verify the output:
cat sorted_data.txt
```
---

### Task 11: Count occurrences of a word in a file
Create a file named `text.txt` with some random content. Use a combination of `cat`, `grep`, and `wc` to count how many times the word "Linux" appears in the file.
```bash
# Command to run:
cat text.txt | grep -o "Linux" | wc -l
```

### Task 12: Redirect stdout to `/dev/null`
Run the `ls` command and redirect its output to `/dev/null` (a special file that discards everything written to it). Check that no output appears in the terminal.
```bash
# Command to run:
ls > /dev/null
```

### Task 13: Create a log of both stdout and stderr
Run a command that generates both output and errors. Redirect stdout to a file called `log.txt` and stderr to the same file, ensuring both are written to the file in the order they appear.
```bash
# Command to run:
ls file_that_exists non_existent_file > log.txt 2>&1
# Verify the output:
cat log.txt
```

### Task 14: Use `tee` to capture stdout and also display it
The `tee` command allows you to redirect output to both the terminal and a file. Use `ls` to list the contents of a directory, then pipe the output through `tee` to save it in `file_list.txt` while still displaying it in the terminal.
```bash
# Command to run:
ls | tee file_list.txt
```

### Task 15: Chaining multiple pipes
Use `cat` to read a file, `grep` to filter lines containing the word "bash", and then pipe the result into `cut` to extract the second field (assuming fields are space-separated). Pipe that into `sort` to sort the output.
```bash
# Command to run:
cat /etc/passwd | grep bash | cut -d ':' -f 1 | sort
```

### Task 16: Redirect output from a background process
Run the `sleep` command in the background, and redirect its output (if any) and errors to a file called `background_output.txt`.
```bash
# Command to run:
sleep 10 > background_output.txt 2>&1 &
# Check the process list:
jobs
```

### Task 17: Compare two files using `diff` and redirect the differences
Create two files, `file1.txt` and `file2.txt`, with some differing content. Use the `diff` command to compare them and redirect the differences to a file called `diff_output.txt`.
```bash
# Command to run:
diff file1.txt file2.txt > diff_output.txt
# Verify the output:
cat diff_output.txt
```

### Task 18: Redirect output of a command inside a loop
Write a `for` loop that runs the `echo` command multiple times, printing "Line X" where `X` is the line number (1 to 5). Redirect the output to a file named `loop_output.txt`.
```bash
# Command to run:
for i in {1..5}; do echo "Line $i"; done > loop_output.txt
# Verify the output:
cat loop_output.txt
```

### Task 19: Chain commands and handle errors
Write a chain of commands where you attempt to list a non-existent file (`ls`), and after it fails, try another command (e.g., `echo`). Redirect the error from `ls` to a file called `errors.txt` and the successful `echo` output to `output.txt`.
```bash
# Command to run:
ls non_existent_file 2> errors.txt || echo "File not found, continuing..." > output.txt
# Verify the output:
cat errors.txt
cat output.txt
```

### Task 20: Use `find` and redirect its output
Use the `find` command to locate all `.txt` files in a directory. Redirect the output to a file named `found_files.txt`.
```bash
# Command to run:
find . -name "*.txt" > found_files.txt
# Verify the output:
cat found_files.txt
```

### Task 21: Capture command output and errors in separate files using grouping
Run a command (like `ls`) and capture its stdout and stderr in separate files, but do it inside a single grouping construct. Use `{}` to group commands together.
```bash
# Command to run:
{ ls file_that_exists; ls non_existent_file; } > output.txt 2> error.txt
# Verify the output:
cat output.txt
cat error.txt
```

### Task 22: Redirect output to multiple files using `tee`
Use the `ls` command to list files in the current directory. Pipe the output to `tee` and redirect it to two files: `file1.txt` and `file2.txt`, while also displaying the output in the terminal.
```bash
# Command to run:
ls | tee file1.txt file2.txt
# Verify the output:
cat file1.txt
cat file2.txt
```

### Task 23: Use `xargs` with redirection
Create a file `file_list.txt` containing the names of several files (one per line). Use `xargs` to read this file and pass the filenames as arguments to the `ls` command. Redirect the output to a file `xargs_output.txt`.
```bash
# Command to run:
cat file_list.txt | xargs ls > xargs_output.txt
# Verify the output:
cat xargs_output.txt
```

### Task 24: Redirecting output of a script
Write a simple shell script `script.sh` that echoes a message and lists a directory. Redirect both stdout and stderr of the script to a log file `script_log.txt`.
```bash
# Create a script:
echo -e '#!/bin/bash\necho "Running script..."\nls /nonexistent' > script.sh
chmod +x script.sh
# Run the script with redirection:
./script.sh > script_log.txt 2>&1
# Verify the output:
cat script_log.txt
```

### Task 25: Count files and redirect the result
Run a command that counts how many files are in the current directory. Redirect the result (the number of files) to a file called `file_count.txt`.
```bash
# Command to run:
ls | wc -l > file_count.txt
# Verify the output:
cat file_count.txt
```
---

