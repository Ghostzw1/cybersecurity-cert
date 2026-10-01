# Course 4 — Operating systems and Linux

**Coverage:** Modules 1–3 covered according to reported progress; Module 4 is [current SQL study](sql-notes.md). This guide adapts two saved personal Linux note files, adds revision explanations, and corrects terminology. Commands below are reference examples, not a transcript of a completed lab.

## Module 1: Operating systems

An operating system manages hardware resources and provides services to applications. The kernel handles core work such as scheduling, memory, and interaction with devices. Applications perform user tasks; the user interacts through an interface such as a graphical desktop or a command shell.

A graphical user interface makes many operations visible through windows and controls. A command-line interface accepts text commands and can support repeatable workflows. Both can perform sensitive actions; a command is not safe simply because it is short.

Windows, macOS, and Linux-based systems differ in their administration tools, permission models, and software ecosystems. A virtual machine provides a guest operating system with virtual hardware. It can be useful for a lab, but isolation still depends on its configuration and how files and networks are shared.

## Module 2: Linux, distributions, and packages

Linux is the kernel; a Linux distribution combines it with utilities, libraries, software management, and other components. Debian, Ubuntu, Kali Linux, Red Hat Enterprise Linux, and Slackware are examples of distributions. They are not package managers. Bash is one common shell; alternatives include Zsh, Korn shell, C shell, and tcsh.

The filesystem is organized under `/`. The Filesystem Hierarchy Standard describes conventions for where categories of files belong; it is not a running component of the operating system. Common locations include `/home` for user home directories, `/etc` for system configuration, and `/var` for variable data such as many logs.

Packages contain software and installation metadata. Dependencies are other packages or components required for that software to work; a package does not necessarily include all its dependencies internally.

| Ecosystem | Lower-level tools or package format | Higher-level management |
|---|---|---|
| Debian-derived systems | `dpkg`, `.deb` packages | APT |
| RPM-based systems | RPM, `.rpm` packages | Tools such as DNF or YUM, depending on distribution and release |

These Debian/Ubuntu-style examples illustrate syntax. They were not run for this portfolio update and should only be used in an authorized environment where package changes are intended.

```bash
apt list --installed
sudo apt install suricata
sudo apt install tcpdump
sudo apt remove suricata
```

Read the package manager's proposed changes before confirming them. A command returning an error after removal is not, alone, a complete check of the software's state; use package information and any relevant service checks. [Ubuntu package management](https://documentation.ubuntu.com/server/how-to/software/package-management/)

### Shell input and output

A shell interprets commands. A command can have options that change its behavior and arguments that supply values such as a file path. Quote a path containing spaces.

Processes use standard input (file descriptor 0), standard output (1), and standard error (2). Input can come from a keyboard, a file, or another process. An ordinary pipe, `|`, connects one command's standard output to the next command's standard input; it does not automatically include standard error. [Bash pipelines](https://www.gnu.org/software/bash/manual/html_node/Pipelines)

```bash
echo "Practice only"
expr 8 + 4
grep -i 'error' server_logs.txt | head -n 5
```

The last example assumes a file named `server_logs.txt` exists. It searches without case sensitivity and limits the displayed matching lines. It does not prove that an error represents a security incident.

`>` redirects output and can overwrite an existing file; `>>` appends. `2>` redirects standard error. Keep original evidence separate from working output. [Bash redirections](https://www.gnu.org/s/bash/manual/html_node/Redirections.html)

## Module 3: Navigate, read, filter, and manage files

An absolute path begins at `/`; a relative path is interpreted from the working directory. `/` is the root directory, while `root` is also the name of a privileged account. These are different concepts.

| Command | Purpose and useful detail |
|---|---|
| `pwd` | Show the current working directory |
| `ls`, `ls -la` | List entries; long format plus hidden entries with `-la` |
| `cd` | Change the shell's working directory |
| `cat` | Write file contents to standard output; consider file size first |
| `head`, `tail` | Show the beginning or end; default is ten lines |
| `grep` | Select lines matching a pattern; `-i` ignores case and `-n` shows line numbers |
| `find` | Locate entries by criteria such as name or file type |
| `mkdir`, `rmdir` | Create a directory; remove an empty directory |
| `touch` | Update timestamps, or create an empty file if it does not exist |
| `cp`, `mv` | Copy; move or rename. Check the destination to avoid replacing data |
| `rm` | Remove files; it normally does not move them to a desktop recycle bin |
| `nano`, `vim`, `emacs` | Edit text when the chosen editor is installed |

Example searches, assuming these practice paths exist:

```bash
find ./practice -type f -name '*.log'
grep -n -i 'failed' ./practice/auth.log
head -n 5 ./practice/auth.log
```

The first command finds matching filenames; the second searches file contents. Quoting `'*.log'` lets `find` receive the pattern rather than having the shell expand it first.

### Authentication, authorization, and permissions

Authentication establishes an identity; authorization determines what that identity may access. Standard Linux mode bits distinguish the owner (`u`), group (`g`), and other (`o`) access classes. `a` addresses all three when changing symbolic permissions. “Other” does not mean everyone.

| Permission | Regular file | Directory |
|---|---|---|
| Read (`r`) | Read contents | List names |
| Write (`w`) | Change contents | Modify entries, normally also requiring search permission |
| Execute (`x`) | Attempt to run as a program | Search/traverse the directory |

Access can also be affected by ACLs, privileges, mount options, and other controls. Deleting a file depends on permissions and restrictions on its parent directory, not just the file's write bit. [GNU mode structure](https://www.gnu.org/s/coreutils/manual/html_node/Mode-Structure.html)

For an ordinary file, the illustrative mode `-rw-r-----` gives the owner read/write access, the group read access, and other users no mode-bit access. In numeric notation, `r=4`, `w=2`, and `x=1`; that example is `640`.

```bash
ls -l report.txt
chmod u=rw,g=r,o= report.txt
ls -l report.txt
```

This example assumes an owned practice file named `report.txt`. The second listing is the verification step: the outcome must be inspected rather than assumed. Do not copy this permission choice onto an unrelated file without checking its required access. [GNU symbolic permissions](https://www.gnu.org/software/coreutils/manual/html_node/Setting-Permissions.html)

### Users, groups, and help

Account administration includes creating an identity, assigning appropriate groups, changing access when duties change, and removing access when it is no longer needed. Commands such as `useradd`, `usermod`, and `userdel` require suitable privileges; defaults and available tools vary by distribution. `sudo` runs an authorized command as another user, often root, according to policy.

Use `whoami` and `id` to inspect the current identity and groups. Consult `man`, `--help`, or shell builtin help for the installed environment before using an unfamiliar option. Read the resulting account and permission state after a change.

## Security tools mentioned in the saved notes

Metasploit, Burp Suite, and John the Ripper are examples associated with security testing. tcpdump and Wireshark analyze network traffic; Autopsy supports digital forensics. Naming these tools records introductory exposure, not hands-on proficiency.

Digital forensics involves collecting and examining digital evidence with attention to integrity, context, and documentation. It is not limited to investigations after a confirmed attack. Penetration testing is an authorized assessment with a defined scope.

## Evidence to add next

For a Linux permissions write-up, save the real starting state, required access, commands, resulting state, and explanation. For a filtering task, explain why the pattern was chosen and what it misses. See the [lab register](../LABS.md) and [corrections](corrections.md).

**Course reference:** [Tools of the Trade: Linux and SQL](https://www.coursera.org/learn/linux-and-sql). See [sources and authorship](../SOURCES.md) for the local-note basis.
