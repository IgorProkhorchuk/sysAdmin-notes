The `kill` command in Unix/Linux systems is used to send signals to processes, allowing you to terminate or control them in various ways. By default, it sends the `SIGTERM` (terminate) signal to gracefully stop a process, but it can be used with different options and signals.

Here's a breakdown of its attributes and options:

### Syntax
```
kill [OPTIONS] <signal or signal_number> <pid>...
```

### Common Options and Attributes

1. **`-l`** (list signals):
   - Displays a list of all signal names.
   - Example: `kill -l` will show all the available signals.

2. **`-s`** (specify signal):
   - Allows you to specify a signal by name instead of a number.
   - Example: `kill -s SIGKILL 1234` sends the `SIGKILL` signal to the process with PID 1234.

3. **`-n`** (signal number):
   - Similar to `-s`, but allows you to specify the signal using its number.
   - Example: `kill -n 9 1234` sends the signal `9` (SIGKILL) to the process with PID 1234.

4. **`-p`** (specify process group ID):
   - Instead of a single process, it can target a process group.
   - Example: `kill -p 1234` sends a signal to the process group with the ID 1234.

5. **`-q`** (queue a signal):
   - Used to send a real-time signal to the process.
   - Example: `kill -q 0 1234` queues a real-time signal `0` for the process 1234.

6. **`-0`** (test existence):
   - Does not send any signal but checks if a process exists.
   - Example: `kill -0 1234` checks whether the process with PID 1234 is running.

### Common Signals Used with `kill`

- **`1` (SIGHUP)**: Hang up. Often used to reload a configuration file.
- **`2` (SIGINT)**: Interrupt from the terminal (like pressing Ctrl+C).
- **`9` (SIGKILL)**: Force kill. Immediately terminates a process and cannot be caught or ignored.
- **`15` (SIGTERM)**: Gracefully terminates the process. This is the default signal.
- **`18` (SIGCONT)**: Continue a stopped process.
- **`19` (SIGSTOP)**: Stop (pause) a process. It can be resumed with SIGCONT.
- **`20` (SIGTSTP)**: Stop a process (Ctrl+Z in the terminal).

### Examples:

1. **Gracefully terminate a process:**
   ```
   kill 1234
   ```

2. **Forcefully kill a process:**
   ```
   kill -9 1234
   ```

3. **Send a hang-up signal to reload configuration:**
   ```
   kill -1 1234
   ```

4. **List all available signals:**
   ```
   kill -l
   ```

5. **Send a real-time signal to process:**
   ```
   kill -s SIGRTMIN 1234
   ```
---

Here is a list of the most commonly used signals in Unix/Linux systems with the `kill` command, along with explanations of their functionality:

### Common Signals

1. **`SIGHUP` (1) – Hangup**  
   - Sent to a process when its controlling terminal is closed. It is commonly used to tell daemons to reload their configuration files without restarting.
   - Example: `kill -1 <pid>`

2. **`SIGINT` (2) – Interrupt**  
   - Sent when a user presses `Ctrl+C` in the terminal. This usually interrupts and terminates a process unless it is handled by the process.
   - Example: `kill -2 <pid>`

3. **`SIGQUIT` (3) – Quit**  
   - Similar to `SIGINT`, but produces a core dump. Sent when a user presses `Ctrl+\` in the terminal.
   - Example: `kill -3 <pid>`

4. **`SIGILL` (4) – Illegal Instruction**  
   - Sent when the CPU detects an illegal, undefined, or invalid machine-language instruction in a process. Typically, it results in the process terminating.
   - Example: `kill -4 <pid>`

5. **`SIGABRT` (6) – Abort**  
   - Sent by the `abort()` function, usually to terminate a program abnormally. This signal cannot be ignored.
   - Example: `kill -6 <pid>`

6. **`SIGFPE` (8) – Floating-Point Exception**  
   - Sent when a process performs an erroneous arithmetic operation, such as division by zero.
   - Example: `kill -8 <pid>`

7. **`SIGKILL` (9) – Kill**  
   - Forces the process to immediately terminate. This signal cannot be caught, blocked, or ignored, making it useful when a process is stuck.
   - Example: `kill -9 <pid>`

8. **`SIGUSR1` (10) – User-Defined Signal 1**  
   - A user-defined signal, commonly used by applications to trigger custom behavior. Its usage is defined by the programmer.
   - Example: `kill -10 <pid>`

9. **`SIGSEGV` (11) – Segmentation Fault**  
   - Sent when a process attempts to access memory incorrectly, usually causing it to terminate with a segmentation fault (segfault).
   - Example: `kill -11 <pid>`

10. **`SIGUSR2` (12) – User-Defined Signal 2**  
   - Another user-defined signal that can be used to trigger custom behavior in applications.
   - Example: `kill -12 <pid>`

11. **`SIGPIPE` (13) – Broken Pipe**  
   - Sent when a process writes to a pipe with no reader. This typically causes the process to terminate unless handled.
   - Example: `kill -13 <pid>`

12. **`SIGALRM` (14) – Alarm Clock**  
   - Sent when a timer set by the `alarm()` function expires. Commonly used for timing operations.
   - Example: `kill -14 <pid>`

13. **`SIGTERM` (15) – Terminate**  
   - Requests a process to terminate gracefully, allowing it to close files, release resources, and perform cleanup. This is the default signal used by `kill`.
   - Example: `kill -15 <pid>` or simply `kill <pid>`

14. **`SIGSTKFLT` (16) – Stack Fault**  
   - Sent when a stack fault occurs on a coprocessor (rare in modern systems).
   - Example: `kill -16 <pid>`

15. **`SIGCHLD` (17) – Child Status Change**  
   - Sent to a parent process when a child process terminates or stops. This is typically handled by system daemons or parent processes managing child processes.
   - Example: `kill -17 <pid>`

16. **`SIGCONT` (18) – Continue**  
   - Tells a process to continue if it has been stopped (e.g., with `SIGSTOP` or `SIGTSTP`). It can resume processes paused with `Ctrl+Z`.
   - Example: `kill -18 <pid>`

17. **`SIGSTOP` (19) – Stop (Cannot Be Ignored)**  
   - Stops a process. Unlike `SIGTSTP`, this signal cannot be ignored or caught by the process.
   - Example: `kill -19 <pid>`

18. **`SIGTSTP` (20) – Terminal Stop (Ctrl+Z)**  
   - Sent when a user presses `Ctrl+Z`, causing the process to stop. It can be resumed with `SIGCONT`.
   - Example: `kill -20 <pid>`

19. **`SIGTTIN` (21) – Background Read Attempt**  
   - Sent when a background process attempts to read from the terminal.
   - Example: `kill -21 <pid>`

20. **`SIGTTOU` (22) – Background Write Attempt**  
   - Sent when a background process attempts to write to the terminal.
   - Example: `kill -22 <pid>`

21. **`SIGURG` (23) – Urgent Condition**  
   - Indicates that "out-of-band" data is available on a socket.
   - Example: `kill -23 <pid>`

22. **`SIGXCPU` (24) – CPU Time Limit Exceeded**  
   - Sent when a process exceeds its CPU time limit.
   - Example: `kill -24 <pid>`

23. **`SIGXFSZ` (25) – File Size Limit Exceeded**  
   - Sent when a process tries to expand a file beyond the maximum allowed size.
   - Example: `kill -25 <pid>`

24. **`SIGVTALRM` (26) – Virtual Alarm Clock**  
   - Sent when a virtual timer set by the `setitimer()` function expires.
   - Example: `kill -26 <pid>`

25. **`SIGPROF` (27) – Profiling Timer Expired**  
   - Sent when a process's profiling timer expires (for measuring CPU time used by the process).
   - Example: `kill -27 <pid>`

26. **`SIGWINCH` (28) – Window Change**  
   - Sent when the window size of the terminal changes (e.g., resizing a terminal window).
   - Example: `kill -28 <pid>`

27. **`SIGIO` (29) – I/O Available**  
   - Sent when I/O is available for a file descriptor, often used in asynchronous I/O operations.
   - Example: `kill -29 <pid>`

28. **`SIGPWR` (30) – Power Failure**  
   - Sent when a power failure occurs. Often used by UPS management software to handle power events.
   - Example: `kill -30 <pid>`

29. **`SIGSYS` (31) – Bad System Call**  
   - Sent when a process makes an invalid system call.
   - Example: `kill -31 <pid>`

30. **`SIGRTMIN` to `SIGRTMAX` – Real-Time Signals**  
   - These are reserved for real-time signals. They are user-defined and used for inter-process communication or custom purposes. The exact numbers of these signals may vary depending on the system.
   - Example: `kill -<number> <pid>` where `<number>` is in the range from `SIGRTMIN` to `SIGRTMAX`.

### Summary Table
| Signal     | Number | Description                           |
|------------|--------|---------------------------------------|
| `SIGHUP`   | 1      | Hangup (terminal close)               |
| `SIGINT`   | 2      | Interrupt (Ctrl+C)                    |
| `SIGQUIT`  | 3      | Quit (Ctrl+\)                         |
| `SIGILL`   | 4      | Illegal instruction                   |
| `SIGABRT`  | 6      | Abort                                 |
| `SIGFPE`   | 8      | Floating-point exception              |
| `SIGKILL`  | 9      | Kill (forcefully terminate)           |
| `SIGUSR1`  | 10     | User-defined signal 1                 |
| `SIGSEGV`  | 11     | Segmentation fault                    |
| `SIGUSR2`  | 12     | User-defined signal 2                 |
| `SIGPIPE`  | 13     | Broken pipe                           |
| `SIGALRM`  | 14     | Alarm clock                           |
| `SIGTERM`  | 15     | Terminate                             |
| `SIGCONT`  | 18     | Continue if stopped                   |
| `SIGSTOP`  | 19     | Stop (cannot be ignored)              |
| `SIGTSTP`  | 20     | Stop (Ctrl+Z)                         |
| `SIGCHLD`  | 17     | Child stopped or terminated           |
| `SIGPWR`   | 30     | Power failure                         |
| `SIGWINCH` | 28     | Window size change                    |
| `SIGRTMIN` | varies | Real-time signal minimum              |

These signals allow fine control over processes, either through normal termination (`SIGTERM`), forced termination (`SIGKILL`), pausing (`SIGSTOP`), or even custom signals (`SIGUSR1`, `SIGUSR2`, `SIGRTMIN`). The ability to catch and handle some of these signals is crucial for writing resilient software in Unix-like systems.
