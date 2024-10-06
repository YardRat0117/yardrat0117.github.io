### Lecture 1 Markdown
- Markdown History
	- 2004 John Gruber
	- 2016 CommonMark & GFM
- Markdown
	- lightweight markup language
	- markdown --parser--> HTML --CSS & browser--> what you see
- Markdown Syntax Standard
	- go through according document
- Markdown Syntax (CommonMark)
	- title syntax (ATX)
	- title syntax (Setext)
	- para syntax
	- list syntax
	- separation line syntax
	- code block syntax
	- inline markup syntax
	- embedded picture syntax
	- link syntax
	- inline HTML syntax
- Markdown Extended Syntax
	- table syntax
	- footnote syntax
	- task list syntax
	- formula syntax (KaTex or MathJax)
	- diagram syntax (mermaid)
- Markdown Editor
	- document
		- VScode + mpe
		- obsidian
	- website
		- **notes** mkdocs docsify
		- **blog** hexo hugo
		- **online slides** reveal-md Slidev
### Lecture 2 LaTeX
- LaTeX History
- LaTeX What You Think Is What You Get
	- Content Over Style
- LaTeX Syntax
	- **Command** begins with `\`
		- case sensitive
		- variable `{}` & `[]`
	- **Comment** begins with `%`
	- **Document Structure**
```LaTeX
\documentclass{article} % Document Class

% preamable: package/macros/document format/etc.
\title{title}
\author{author}
\date{date}

\begin{document} % Document Begins
% body: document's content

Hello, \LaTeX{}!
\par % Paragraph Separation
Hello, world!

% Later to Work On
\newline
\newpage

{\bfseries bold}
\textbf{bold}

\linespread
\hspace
\vspace
\quad \qquad

\begin{environment}
% itemize/enumerate/description
\end{environment}

% Inline Formula
$e^{i\pi} + 1 = 0$
\[e^{i\pi} + 1 = 0\]
\left{equation}\right{equation}
\left{align}\right{align}


\end{document}
```
### Lecture 3 Shell & CLI
- Linux
	- Common OS
		- Microsoft Windows
		- macOS
		- Linux
	- Why Not Windows
		- Inefficiency
		- Not suitable for developing
		- Closed-source commercial paid software
		- Hardware Incompatibility
		- Stability & security
	- GUI History
		- What before? Disk Operating Systems (DOS)
			- Apple DOS
			- MS-DOS
		- Xerox PARC: Xerox Alto
		- Steve Jobs: Apple Lisa
		- X.Org Foundation: X11
		- Microsoft: Windows 1.0
		- What after? 
			- Aqua, GNOME, KDE, LXDE, Xfce, etc.
	- Why Linux
		- Open-source kernel & community maintaining
		- Free *as in Free Bear and Free Speech*
		- Lightweight
		- Stability
		- Hardware compatibility
	- Common Linux Release
		- Slackware
		- Debian
		- Arch Linux
		- Ubuntu
		- Deepin
		- Red Hat Enterprise Linux
		- Kali Linux
- Shell / Terminal
	- Terminal
		- Terminal Emulator
		- Shell run inside terminal 
		- Common Terminal
			- Windows: Windows Terminal
			- Linux: Gnome Terminal, Konsole, LXTerminal, etc.
			- macOS: Terminal.app, iTerm2, etc.
			- multi-platform
				- Alacrity: based on Rust
				- Warp: based on Rust
				- Hyper: based on Electron
	- Shell
		- Interface used for user-system-interaction
		- Receive and parse input, return the output after the operation system's execution
		- Common shell
			- Windows: cmd.exe, PowerShell 5
			- Unix-Like Systems
				- sh: Bourne Shell
				- bash: Bourne Again Shell
				- zsh: Z Shell
				- fish: Friendly Interactive Shell
				- etc.
- Shell Basic Command
	- Prompt
		- Username
		- Hostname
		- Current directory
	- Path-related command
		- `pwd` print working directory
		- `cd path` change directory
			- `path` can be either a relative path or an absolute path
			- `~` for `home`, `.` for current directory, `..` for parent directory
	- File/Directory Operating Command
		- `ls [-a] [-l]`
		- `touch {filename}`
		- `mkdir {dir}`
		- `cp {src} {dst} [-r]`
		- `mv {src} {dst}`
		- `rm {files} [-r] [-f]`
		- `find {path} [-name] {pattern}`
	- File Content Command
		- `cat {files} [-n]`
		- `head {file} [-n] {lines}`
		- `tail {file} [-n] {lines}`
		- `more/less {file}`
		- `hexdump {file} [-C] [-n] {N}`
	- Other Command
		- `man`
		- `echo`
		- `whoami`
		- `whereis/which/whence`
		- `clear`
		- `chmod`
		- `ps`
		- `date`
		- `kill`
		- `grep`
		- `diff`
		- `curl`
- Shell Advance
	- Redirect
		- File redirect
		- `stdin stdout stderr`
		- `> {file}` to redirect `stdout` to file, `< {file}` to redirect file to `stdin`
		- `2> {file}` to redirect `stderr` to file
		- `>>` implies `append mode`
		- `&> {file}` to redirect `stdout` and `stderr` to file
	- Pipe
		- The pipe operator `|` connects the left command's `stdout` to the right command's `stdin`
	- Environment Variable
		- `echo ${var}` & `env`
		- `export {var} = {value}`
		- `unset {var}`
	- Settings
- vim
	- #todo 
- GNU make
	- #todo 
- Common CLI Tools (omitted)