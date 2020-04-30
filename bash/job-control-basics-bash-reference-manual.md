# Job Control Basics \(Bash Reference Manual\)

## 7.1 Job Control Basics

Job control refers to the ability to selectively stop \(suspend\) the execution of processes and continue \(resume\) their execution at a later point. A user typically employs this facility via an interactive interface supplied jointly by the operating system kernel’s terminal driver and Bash.

The shell associates a job with each pipeline. It keeps a table of currently executing jobs, which may be listed with the `jobs` command. When Bash starts a job asynchronously, it prints a line that looks like:

indicating that this job is job number 1 and that the process ID of the last process in the pipeline associated with this job is 25647. All of the processes in a single pipeline are members of the same job. Bash uses the job abstraction as the basis for job control.

To facilitate the implementation of the user interface to job control, the operating system maintains the notion of a current terminal process group ID. Members of this process group \(processes whose process group ID is equal to the current terminal process group ID\) receive keyboard-generated signals such as `SIGINT`. These processes are said to be in the foreground. Background processes are those whose process group ID differs from the terminal’s; such processes are immune to keyboard-generated signals. Only foreground processes are allowed to read from or, if the user so specifies with `stty tostop`, write to the terminal. Background processes which attempt to read from \(write to when `stty tostop` is in effect\) the terminal are sent a `SIGTTIN` \(`SIGTTOU`\) signal by the kernel’s terminal driver, which, unless caught, suspends the process.

If the operating system on which Bash is running supports job control, Bash contains facilities to use it. Typing the suspend character \(typically ‘^Z’, Control-Z\) while a process is running causes that process to be stopped and returns control to Bash. Typing the delayed suspend character \(typically ‘^Y’, Control-Y\) causes the process to be stopped when it attempts to read input from the terminal, and control to be returned to Bash. The user then manipulates the state of this job, using the `bg` command to continue it in the background, the `fg` command to continue it in the foreground, or the `kill` command to kill it. A ‘^Z’ takes effect immediately, and has the additional side effect of causing pending output and typeahead to be discarded.

There are a number of ways to refer to a job in the shell. The character ‘%’ introduces a job specification \(jobspec\).

Job number `n` may be referred to as ‘%n’. The symbols ‘%%’ and ‘%+’ refer to the shell’s notion of the current job, which is the last job stopped while it was in the foreground or started in the background. A single ‘%’ \(with no accompanying job specification\) also refers to the current job. The previous job may be referenced using ‘%-’. If there is only a single job, ‘%+’ and ‘%-’ can both be used to refer to that job. In output pertaining to jobs \(e.g., the output of the `jobs` command\), the current job is always flagged with a ‘+’, and the previous job with a ‘-’.

A job may also be referred to using a prefix of the name used to start it, or using a substring that appears in its command line. For example, ‘%ce’ refers to a stopped `ce` job. Using ‘%?ce’, on the other hand, refers to any job containing the string ‘ce’ in its command line. If the prefix or substring matches more than one job, Bash reports an error.

Simply naming a job can be used to bring it into the foreground: ‘%1’ is a synonym for ‘fg %1’, bringing job 1 from the background into the foreground. Similarly, ‘%1 &’ resumes job 1 in the background, equivalent to ‘bg %1’

The shell learns immediately whenever a job changes state. Normally, Bash waits until it is about to print a prompt before reporting changes in a job’s status so as to not interrupt any other output. If the -b option to the `set` builtin is enabled, Bash reports such changes immediately \(see [The Set Builtin](the-set-builtin-bash-reference-manual.md#The-Set-Builtin)\). Any trap on `SIGCHLD` is executed for each child process that exits.

If an attempt to exit Bash is made while jobs are stopped, \(or running, if the `checkjobs` option is enabled – see [The Shopt Builtin](the-shopt-builtin-bash-reference-manual.md#The-Shopt-Builtin)\), the shell prints a warning message, and if the `checkjobs` option is enabled, lists the jobs and their statuses. The `jobs` command may then be used to inspect their status. If a second attempt to exit is made without an intervening command, Bash does not print another warning, and any stopped jobs are terminated.

When the shell is waiting for a job or process using the `wait` builtin, and job control is enabled, `wait` will return when the job changes state. The -f option causes `wait` to wait until the job or process terminates before returning.

