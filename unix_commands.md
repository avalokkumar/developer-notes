### Linux Commands

1. `kill` - This command sends a signal to a specific process to terminate it. For example, "kill 1234" will send a signal to terminate the process with ID 1234.
2. `killall` - This command sends a signal to all processes with a specified name to terminate them. For example, "killall firefox" will send a signal to terminate all processes with the name "firefox".
3. `nice` - This command is used to change the priority of a process. For example, "nice -20 firefox" will run the "firefox" process with a higher priority.
4. `sleep` - This command is used to pause the execution of a script for a specified number of seconds. For example, "sleep 5" will pause the script for 5 seconds before continuing execution.
5. `watch` - This command is used to repeatedly execute a command at a specified interval. For example, "watch -n 5 ls -l" will execute the "ls -l" command every 5 seconds.
6. `crontab` - This command is used to schedule jobs to be executed automatically at specified intervals. For example, "crontab -e" will open the crontab configuration file, where you can add a line like "30 2 * * * /path/to/script.sh" to run "script.sh" everyday at 2:30 AM.
7. `host` - This command is used to look up the IP address(es) associated with a hostname. For example, "host google.com" will return the IP addresses associated with the domain "google.com".
8. `whois` - This command is used to look up information about a domain or IP address. For example, "whois google.com" will return information about the ownership and registration of the domain "google.com".
9. `ping` - This command is used to test the reachability of a host and measure the round-trip time for packets sent to the host. For example, "ping google.com" will send a series of packets to "google.com" and display the round-trip time for each packet.
10. `traceroute` - This command is used to trace the path packets take to a destination host. For example, "traceroute google.com" will display the path packets take to reach "google.com".
11. `ssh` - This command is used to securely log in to a remote machine. For example, "ssh user@hostname" will log in to the machine "hostname" as the user "user".
12. `telnet` - This command is used to establish a Telnet connection to a remote machine. For example, "telnet hostname" will establish a Telnet connection to the machine "hostname".
13. `scp` - This command is used to securely copy files between machines. For example, "scp file.txt user@hostname:/path/to/destination" will copy the file "file.txt" to the machine "hostname" in the directory "/path/to/destination" as the user "user".
14. `ftp` - This command is used to transfer files to and from a remote machine using the File Transfer Protocol. For example, "ftp hostname" will connect to the machine "hostname" and open an FTP prompt where you can issue commands like "get" to download a file and "put" to upload a file.
15. `echo` - This command is used to display a line of text in the terminal. For example, "echo "Hello, world!"" will display the text "Hello, world!" in the terminal.
16. `printf` - This command is similar to echo, but it allows for more advanced formatting options. For example, "printf "The value of pi is %.2f" 3.1415" will display the text "The value of pi is 3.14" in the terminal.

17. `seq` - This command is used to generate a sequence of numbers. For example, "seq 5 10" will display the numbers 5, 6, 7, 8, 9, 10 in the terminal.
18. `clear` - This command is used to clear the terminal screen. This will remove all previous command outputs and bring the cursor to the top of the screen. For example, "clear" will clear the terminal screen.
19. `ps` - This command is used to display information about currently running processes. For example, "ps aux" will display information about all running processes on the system.
20. `uptime` - This command is used to display the amount of time the system has been running. For example, "uptime" will display the amount of time the system has been running.
21. `top` - This command is used to display real-time information about running processes, including their resource usage. For example, "top" will display real-time information about running processes and their resource usage
22. `cp` - This command is used to copy files and directories. For example, "cp file.txt newfile.txt" will create a copy of "file.txt" as "newfile.txt" in the same directory.
23. `mv` - This command is used to move or rename files and directories. For example, "mv oldfile.txt newfile.txt" will rename "oldfile.txt" to "newfile.txt".
24. `rm` - This command is used to remove files and directories. For example, "rm file.txt" will delete the file "file.txt".
25. `mkdir` - This command is used to create new directories. For example, "mkdir newfolder" will create a new directory called "newfolder".
26. `rmdir` - This command is used to remove empty directories. For example, "rmdir emptyfolder" will delete the empty directory "emptyfolder".
27. `ls` - This command is used to list the files and directories in a directory. For example, "ls" will list the files and directories in the current directory.
28. `cd` - This command is used to change the current working directory. For example, "cd /home/user" will change the current working directory to "/home/user".
29. `df` - This command is used to display the amount of free space on file systems. For example, "df -h" will display the amount of free space on file systems in human-readable format.
30. `du` - This command is used to display the amount of disk space used by files and directories. For example, "du -sh *" will display the amount of disk space used by all files and directories in the current directory in human-readable format.
31. `grep` - This command is used to search for a specific pattern in a text file. For example, "grep "error" logfile.txt" will search for the word "error" in the file "logfile.txt".
32. `find` - This command is used to search for files and directories in a specific location. For example, "find / -name "file.txt"" will search for a file called "file.txt" in the root directory and all its subdirectories.
33. `tar` - This command is used to create and extract archive files. For example, "tar -cvf archive.tar /path/to/files" will create an archive file called "archive.tar" containing the files located at "/path/to/files".
34. `gzip` - This command is used to compress and decompress files. For example, "gzip file.txt" will compress the file "file.txt" and create a new file called "file.txt.gz".
35. `unzip` - This command is used to extract files from a zip archive. For example, "unzip archive.zip" will extract all the files from the archive "archive.zip".
36. `chmod` - This command is used to change the permissions of a file or directory. For example, "chmod 755 file.txt" will give read, write and execute permissions to the owner and read and execute permissions to group and others for the file "file.txt".
37. `chown` - This command is used to change the ownership of a file or directory. For example, "chown user:group file.txt" will change the ownership of the file "file.txt" to the user "user" and the group "group".
38. `df` - This command is used to display the amount of free space on file systems. For example, "df -h" will display the amount of free space on file systems in human-readable format.
39. `free` - This command is used to display the amount of free and used memory in the system.
40. `df` - This command is used to check the disk usage of the file system
41. `lsof` - This command is used to list open files and the processes that have them open. For example, "lsof -i :80" will list all the processes that have open files associated with the port 80.
42. `dmesg` - This command is used to display the kernel ring buffer. It shows the messages generated by the kernel and other system processes. For example, "dmesg" will display all the messages in the kernel ring buffer.
43. `htop` - This command is an interactive process viewer similar to top command. It shows real-time process list in a user-friendly interface. For example, "htop" will display all the processes running on the system in real-time.
44. `netstat` - This command is used to display network connections, routing tables, interface statistics and more. For example, "netstat -tuln" will display all the active TCP connections and their associated listening ports.
45. `route` - This command is used to show or manipulate the IP routing table. For example, "route -n" will display the current routing table of the system without resolving hostnames.
46. `dig` - This command is used to perform DNS lookups. For example, "dig google.com" will display the DNS information for the domain "google.com".
47. `nslookup` - This command is used to query DNS servers for information. For example, "nslookup google.com" will query the DNS server for information about the domain "google.com".
48. `ifconfig` - This command is used to configure network interfaces and display their status. For example, "ifconfig" will display information about all the active network interfaces on the system.
49. `w` - This command is used to display information
about the currently logged-in users and their processes. For example, "w" will show the list of logged-in users, their terminal, login time, idle time and the processes they are running.
50. `history` - This command is used to display the command history of the current session. For example, "history" will show a list of previously executed commands in the current terminal session.



----

#### some commands might be repeated

22. free - This command is used to display information about the system's memory usage, including the amount of free, used, and total memory.

23. killall5 - This command sends a signal to all processes, except process with process-id 1 (init), to terminate them.

24. renice - This command is used to change the priority of a running process.

25. at - This command is used to schedule a command or script to run at a specific time in the future.

26. cron - This command is used to schedule repetitive tasks, it's similar to crontab but doesn't require to be invoked via crontab -e.

27. nslookup - This command is used to query DNS servers for information about a domain or IP address.

28. dig - This command is similar to nslookup, it's used to query DNS servers for information about a domain or IP address, it's more powerful than nslookup and can be used for more complex queries.

29. netstat - This command is used to display information about network connections, including open sockets and routing tables.

30. nc - This command is used to open a TCP or UDP connection to a remote host.

31. rsync - This command is used to synchronize files and directories between two locations, it can work over SSH and is more efficient than scp when dealing with large number of files.

32. tcpdump - This command is used to capture and analyze network traffic.

33. iptables - This command is used to configure the Linux kernel's built-in firewall.

34. systemctl - This command is used to manage and control system services on Linux, it can be used to start, stop, enable, disable, and check the status of services.

35. df - This command is used to display information about the amount of free space on file systems.

36. du - This command is used to display the amount of space used by a directory and its subdirectories.

37. lsof - This command is used to display information about open files and the processes that have them open.

38. strace - This command is used to trace system calls and signals of a process.

39. ltrace - This command is similar to strace, it traces library calls of a process.

40. htop - This command is similar to top, it's an interactive process viewer that shows a frequently updated list of processes running on a system, it's more user-friendly than top.

41. w - This command is used to display information about logged-in users and their processes.

42. last - This command is used to display information about previous logins on the system.

43. find - This command is used to search for files and directories based on various criteria, such as name, size, and timestamp.

44. grep - This command is used to search for patterns in text files.

45. sed - This command is used to perform basic text transformations on an input stream (a file or input from a pipeline).

46. awk - This command is similar to sed, it's used to perform basic text transformations on an input stream, it's more powerful than sed and it can handle more complex transformations.

47. tar - This command is used to create and extract archives of files.

48. gzip - This command is used to compress or decompress files.

49. zip - This command is similar to gzip, it's used to compress and extract files, it's more powerful than gzip and it can handle more compression formats.

50. unzip - This command is used to extract files from a zip archive.

51. chmod - This command is used to change the permissions of a file or directory.

52. chown - This command is used to change the ownership of a file or directory.

53. ln - This command is used to create links between files and directories.

54. mv - This command is used to move or rename files and directories.

55. cp - This command is used to copy files and directories.

56. rm - This command is used to delete files and directories.

57. touch - This command is used to update the timestamp of a file or create an empty file if it does not exist.

58. dd - This command is used to perform low-level operations on storage devices, such as copying, formatting, and cloning.

59. md5sum - This command is used to generate and check MD5 message digests.

60. sha1sum - This command is similar to md5sum, it's used to generate and check SHA-1 message digests.

61. diff - This command is used to compare the contents of two files or directories.

62. patch - This command is used to apply patches to files.
