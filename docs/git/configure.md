---
layout: default
title: git
date: 31 08 2024
author: GG
tags: config
---

Install Windows / Scoop
---

``` zsh
scoop install --global git
```

Configure global settings
---

``` zsh
git config --global --get core.autocrlf
```

The git hardclean alias will discard all uncommitted changes and delete 
untracked files and directories, including added folders and files.

``` zsh
git config --global alias.hardclean '!git reset --hard && git clean -fd'
```

See how to set up a compare or a merge tool like kdiff3 or meld

Configure settings for a specific repo
---

``` zsh
git config user.email "x.y@z.com"
git config user.name "X Y"
```

Reset submodules to the original state
---

``` zsh
git submodule deinit -f .
git submodule update --init

```

Find all git repos in a folder
---

``` zsh
find . -type d -name ".git" -exec dirname {} \; | sort -u
```

Handling Case-Sensitivity Issues on Case-Insensitive File Systems
---

This problem can arise when working on file systems where casing is ignored 
(e.g., Windows or macOS). In such environments, files with the same name but 
different casing (e.g., MyFile.txt and myfile.txt) can create inconsistencies 
between Git (which is case-sensitive) and the file system (which is not).

The script below lists the problematic filenames as git mv commands, which fix
the casing issues by aligning the filenames in Git with those in the file 
system.

Script: git_check_casing.py

```python
import os
import subprocess

def get_git_files():
    """Get the list of versioned files from Git."""
    result = subprocess.run(['git', 'ls-tree', '-r', 'HEAD', '--name-only'], stdout=subprocess.PIPE, text=True)
    git_files = result.stdout.splitlines()
    return git_files

def get_filesystem_files():
    """Get the list of all files in the filesystem starting from the current directory."""
    for root, dirs, files in os.walk("."):
        for file in files:
            filepath = os.path.relpath(os.path.join(root, file), ".")
            filesystem_files.append(filepath)
    return filesystem_files

def find_case_sensitive_mismatches(git_files, filesystem_files):
    """Find files that match ignoring case but differ in case sensitivity."""
    git_files_lower = {file.lower().strip(): file for file in git_files}
    filesystem_files_lower = {file.lower().strip(): file for file in filesystem_files}

    for file_lower, git_file in git_files_lower.items():
        if file_lower in filesystem_files_lower:
            filesystem_file = filesystem_files_lower[file_lower]
            if git_file != filesystem_file:
                # Strip carriage return or newline characters
                git_file_clean = git_file.strip()
                filesystem_file_clean = filesystem_file.strip()
                # Output the git mv command to fix the case mismatch
                print(f'git mv "{git_file_clean}" "{filesystem_file_clean}"')

if __name__ == "__main__":
    git_files = get_git_files()
    filesystem_files = get_filesystem_files()

    find_case_sensitive_mismatches(git_files, filesystem_files)
```