# Review of saved Linux notes

Two personal text-note files for Modules 2 and 3 were used to prepare the [Linux guide](notes.md). The revisions below make the explanations more precise. They document an AI-assisted editing review, not errors encountered in an executed lab.

| Topic | Clarification applied |
|---|---|
| Linux architecture | Linux is the kernel; a distribution combines it with other software. The kernel manages more than memory alone. |
| Filesystem hierarchy | FHS is a standard describing directory conventions, not a software component. |
| Distribution names | Red Hat Enterprise Linux is one name. Slackware is the correct spelling. |
| Package management | Ubuntu and Kali are distributions; APT, dpkg, RPM, and related tools manage packages. Dependencies may be installed separately. |
| Lifecycle information | An old claim about CentOS releases was not retained as current guidance. Support information must be checked for the exact distribution and release. |
| Package syntax | The package name is `tcpdump`; the illustrative installation command is `sudo apt install tcpdump`. |
| Shell streams | Input, output, and errors are process streams; they are not limited to information typed by a person or returned by the OS. |
| Pipe | The operator is `|`; ordinary piping passes stdout, not automatically stderr. |
| Text search | `grep` normally selects matching lines from input; `find` locates entries using filesystem criteria. |
| File operations | `rmdir` removes empty directories. `touch` also updates timestamps. Copy and move can overwrite destinations. |
| Permission listing | The command is `ls -l`; `ls -la` also includes hidden entries. |
| Permission classes | Group is `g`. Other is `o`; all is `a`. File and directory permissions have different effects. |
| Verification | Inspect actual package, file, or account state after a change; do not substitute an expected result for observed output. |

Technical references are linked next to the corresponding explanations in the [Linux guide](notes.md). The saved notes establish study material; they do not establish completion of particular labs.
