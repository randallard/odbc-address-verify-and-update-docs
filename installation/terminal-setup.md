---
layout: page
title: Terminal Setup
---

### note
this still needs verified

# Terminal Setup Instructions

These are instructions on setting up the terminal for best use

## Add alias 'avu'

### For PowerShell:

Open your PowerShell profile file (usually located at $PROFILE).
Add the following line to create an alias:

```powershell
New-Alias -Name avu -Value "path\to\your\program.exe"
```

Replace "path\to\your\program.exe" with the actual path to your compiled Rust program.

### For Linux:

Open your shell configuration file (e.g., ~/.bashrc for Bash or ~/.zshrc for Zsh).

Add the following line to create an alias:

```bash
alias avu='path/to/your/program'
```

Replace 'path/to/your/program' with the actual path to your compiled Rust program.