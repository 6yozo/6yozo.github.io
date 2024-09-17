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
git config --global core.ignorecase false
```

- Line Endings: The `core.autocrlf` setting helps Git automatically handle line
  endings, which improves cross-platform development by converting line endings 
  between Windows (CRLF) and Unix-based systems (LF) as needed.

- Case Sensitivity: Setting `core.ignorecase=false` ensures that Git respects 
  filename casing, making the repository more cross-platform friendly. 
  On case-insensitive systems like Windows, Git might otherwise ignore case 
  changes (e.g., File.txt vs. file.txt), which can cause inconsistencies. 
  
Set up aliases
---

The git hardclean alias will discard all uncommitted changes and delete 
untracked files and directories, including added folders and files.

``` zsh
git config --global alias.hardclean '!git reset --hard && git clean -fd'
git config --global alias.lfi 'log HEAD --graph --all --abbrev-commit --full-history --color --pretty=format:\'"%Cred%h%Creset -%C(yellow)%d%Creset %s%Cgreen(%cr) %C(bold blue)<%an>%Creset\' --date=relative'
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

#### Case Sensitivity on Windows

When developing cross-platform applications on Windows, enabling case 
sensitivity for both the filesystem and Git can prevent issues related to 
differing file name casing across platforms.

##### Enabling Case Sensitivity in the Filesystem

By default, Windows treats files as case-insensitive. However, you can 
enable case sensitivity for specific directories on Windows 10 and later. 
This ensures that files with names differing only by case 
(e.g., file.txt and File.txt) are treated as distinct files.

To enable case sensitivity for a specific folder, run the following 
command in a Command Prompt with administrator privileges:

```pwshell
fsutil file setCaseSensitiveInfo C:\Path\To\Someplace enable
```

##### Configuring Git to Respect Case Sensitivity

After enabling case sensitivity on the filesystem, ensure that Git also 
respects the file name casing by setting core.ignorecase to false. This
ensures Git tracks file name changes involving only case differences.

```zsh
git config core.ignorecase false
```

#### Approach 1 to fix casing 

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

#### Approach 2 to fix casing 

The fix_casing.py script automates the process of aligning the casing of 
filenames between the filesystem and Git in a case-insensitive environment
(such as Windows). It ensures that Git respects the correct file casing and
resolves potential issues caused by case-insensitive file systems.

Process Overview:

Disable Git's Case Sensitivity Temporarily:

Git's core.ignorecase setting is temporarily set to true to allow operations 
that might involve case-insensitive file handling during the execution of the 
script. 

Switch to Target Branch:

The script switches to the target branch specified by the user. This ensures
the correct context for resolving casing differences.

Retrieve Files from Filesystem and Git:

The script gathers all files in the current working directory (the repository)
and records their correct casing as they appear in the filesystem.
It also retrieves the list of files tracked by Git in the current branch 
using git ls-tree.

Compare Casing:

The script compares the casing of files in Git with those on the filesystem:
If a file exists in Git but not in the filesystem, an error is raised, 
and the process is aborted. If a file exists both in Git and the filesystem but the casing differs, 
the file is marked for correction.

Fix File Casing:

For files with mismatched casing, the script renames them using git mv. 
It temporarily renames the file to avoid conflicts, then renames it back to 
the correct casing based on the filesystem.

Commit Changes:

If any file renaming occurred, the script commits the changes automatically 
with the message: "Fix casing for files and  directories based on filesystem".
If no changes were needed, the commit step is skipped.

Restore Git Case Sensitivity:

After processing, the script resets the Git core.ignorecase setting to
false, ensuring Git tracks file names with case sensitivity.

Error Handling:

If an error occurs at any point during the execution, the script ensures 
Git's case sensitivity (core.ignorecase) is restored to its original value
and the process is aborted gracefully.

```python
import subprocess
import sys
import os

# Helper function to run a Git command
def run_git_command(command, check=True):
    try:
        result = subprocess.run(command, check=check, stdout=subprocess.PIPE, stderr=subprocess.PIPE, text=True)
        return result.stdout.strip()
    except subprocess.CalledProcessError as e:
        print(f"Error running command: {' '.join(command)}")
        print(e.stderr)
        sys.exit(1)

# Function to restore Git case sensitivity and exit
def restore_case_sensitivity():
    print("Restoring Git case sensitivity...")
    run_git_command(["git", "config", "core.ignorecase", "false"])
    sys.exit(1)

# Function to get all files from the filesystem (relative to the Git directory)
def get_filesystem_files():
    filesystem_files = []
    for root, dirs, files in os.walk("."):
        for name in files:
            # Append relative paths with correct casing
            relative_path = os.path.join(root, name).replace("./", "")
            filesystem_files.append(relative_path)
    return filesystem_files

# Function to get the list of files from Git (relative to the Git directory)
def get_git_files():
    git_files = run_git_command(["git", "ls-tree", "-r", "HEAD", "--name-only"]).splitlines()
    return git_files

# Function to compare Git and filesystem casing
def compare_casing(filesystem_files, git_files):
    files_to_fix = []

    # Create sets for faster lookups
    git_files_lower = {f.lower() for f in git_files}
    filesystem_files_lower = {f.lower() for f in filesystem_files}

    # Check if any files in Git are missing from the filesystem
    for git_file in git_files:
        if git_file.lower() not in filesystem_files_lower:
            print(f"Error: File in Git but not on filesystem: {git_file}")
            restore_case_sensitivity()

    # Compare the two lists for case differences
    for fs_file in filesystem_files:
        if fs_file.lower() in git_files_lower:
            matching_git_file = next(git_file for git_file in git_files if git_file.lower() == fs_file.lower())
            if fs_file != matching_git_file:
                print(f"Case mismatch: {matching_git_file} -> {fs_file}")
                files_to_fix.append((matching_git_file, fs_file))

    return files_to_fix

# Function to fix casing of files
def fix_case(git_file, correct_case):
    if os.path.exists(correct_case):
        temp_path = git_file + "_temp"
        # Use git mv to force the casing change (rename to temp and back to correct)
        run_git_command(["git", "mv", "-f", git_file, temp_path])
        run_git_command(["git", "mv", "-f", temp_path, correct_case])
        print(f"Fixed case for: {git_file}")
    else:
        print(f"Error: File not found on filesystem: {correct_case}")
#        restore_case_sensitivity()

# Main function to handle the process
def main(branch_name):
    if not branch_name:
        print("Please provide a target branch name")
        sys.exit(1)

    # Step 1: Temporarily disable Git case sensitivity
    print("Temporarily disabling Git case sensitivity...")
    run_git_command(["git", "config", "core.ignorecase", "true"])

    # Step 2: Checkout the target branch
    print(f"Checking out branch: {branch_name}")
    run_git_command(["git", "checkout", branch_name])

    # Step 3: Get list of files from filesystem and Git
    filesystem_files = get_filesystem_files()
    git_files = get_git_files()

    # Step 4: Compare casing between filesystem and Git
    files_to_fix = compare_casing(filesystem_files, git_files)

    # Step 5: Fix the casing for files and directories that need it
    for git_file, correct_case in files_to_fix:
        fix_case(git_file, correct_case)

    # Step 6: Commit the changes if there are any
    status_output = run_git_command(["git", "status", "--porcelain"])

    if status_output:
        print("Committing changes to fix casing for files and directories...")
        run_git_command(["git", "commit", "-m", "Fix casing for files and directories based on filesystem"])
    else:
        print("No changes to commit. Skipping commit.")

    # Step 7: Re-enable Git case sensitivity
    print("Re-enabling Git case sensitivity...")
    run_git_command(["git", "config", "core.ignorecase", "false"])

    print("Process complete!")

# Run the script
if __name__ == "__main__":
    if len(sys.argv) < 2:
        print("Usage: python fix_casing.py <branch_name>")
        sys.exit(1)

    target_branch = sys.argv[1]
    try:
        main(target_branch)
    except Exception as e:
        print(f"An error occurred: {e}")
        restore_case_sensitivity()
```