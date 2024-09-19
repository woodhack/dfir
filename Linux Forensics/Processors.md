# Processors

Processes are instances of programs that are currently running on your machine. They are managed by the kernel, which is the core part of the operating system. Each process is assigned a unique identifier called a **Process ID** or **PID**. The PID is incremented based on the order in which processes start, meaning the first process gets a low PID, and subsequent processes get higher PIDs.

The operating system uses **namespaces** and **cgroups** (control groups) to manage how processes interact with system resources, such as CPU, RAM, and I/O. Namespaces isolate the process’s view of the system, ensuring processes have their own independent resources like file systems, network interfaces, or user IDs. Cgroups allow the OS to set limits and priorities for resource usage by these processes.

The process with an ID of 0 is the **swapper** or **idle** process, which is created when the system boots. Its primary task is to manage idle CPU time when no processes require it. The first user-space process, with an ID of 1, is called **init**, responsible for starting other processes during system startup. On most modern Linux distributions like Ubuntu, this role is taken by **systemd**, which acts as the system and service manager. It provides an interface to manage system services and user processes, effectively sitting between the OS and the user.

### Processes at Boot

Some applications, such as web servers (e.g., Apache), database servers (e.g., MySQL), or file transfer services (e.g., vsftpd), are often critical and designed to start automatically at boot. Administrators typically configure these services to run at startup because they are essential to the server's operation. These services are often managed by **systemd** using unit files that define how and when they should start, stop, or restart.

### Foreground and Background Processes

Processes can run in either the **foreground** or the **background**. Foreground processes interact directly with the user. For instance, commands you run in your terminal, like `echo`, run in the foreground, meaning they hold control of the terminal until they finish. Background processes, on the other hand, run behind the scenes without direct user interaction. You can move a running process to the background by appending an `&` to the command or by using process control commands like `bg` to resume a suspended process in the background.

### Monitoring and Managing Processes

Understanding and managing processes is essential for system administration and forensics. Here are some important commands and signals for process management:

- **ps**: Displays a list of running processes. It shows information such as the PID, the terminal (TTY) from which it was started, the CPU usage, and the command that initiated the process.
    
    `ps`
    
- **ps aux**: This variation of `ps` provides a more comprehensive list of all processes running on the system, including those not started from the current terminal session. It also shows processes owned by other users and system processes.
    
    `ps aux`
    
- **top**: Displays real-time information about the system's processes, including CPU and memory usage, process priority, and uptime. It updates dynamically and is useful for monitoring the system's health over time.
    
    `top`
    
- **htop**: Similar to `top` but with a more user-friendly interface, `htop` provides interactive real-time monitoring of processes. It allows you to navigate through processes and even kill them directly from the interface.
    
    `htop`
    
- **kill {PID}**: Sends a signal to a process, typically to terminate it. There are different signals you can send depending on how you want to stop or control the process:
    - **SIGTERM (15)**: This signal requests the process to gracefully terminate, allowing it to perform cleanup tasks (e.g., saving data, closing files).
    - **SIGKILL (9)**: This is a forceful termination signal that immediately stops the process without allowing it to perform any cleanup.
    - **SIGSTOP (19)**: This signal stops (pauses) a process without terminating it, effectively suspending its operation. You can later resume it using **SIGCONT**.
    
    Example usage:
    
    `kill {PID}`
    
    `kill -9 {PID}`
    

### Process States

Processes in Linux can be in various states:

- **Running (R)**: The process is currently being executed by the CPU.
- **Sleeping (S)**: The process is waiting for a resource or an event to complete (e.g., waiting for I/O operations to finish).
- **Stopped (T)**: The process has been stopped, either by a signal or because it was suspended by the user or system.
- **Zombie (Z)**: A zombie process is one that has completed execution but still has an entry in the process table because the parent process has not yet read its exit status.

You can identify these process states using the `ps` command.

### Process Priorities and Niceness

In Linux, processes can have different priorities based on how critical they are or how much CPU time they require. The **niceness** value determines the scheduling priority of a process. Lower niceness values give a process higher priority, while higher values reduce priority. You can change the niceness value of a running process using the **nice** or **renice** command:

- **nice**: Starts a process with a specific niceness level.
    
    `nice -n 10 command`
    
- **renice**: Adjusts the niceness value of an already running process.
    
    `renice 5 {PID}`