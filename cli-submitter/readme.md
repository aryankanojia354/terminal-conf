# Codeforces Submitter Script (For Linux)

## Installation Instructions

Follow these steps to install and configure the Codeforces submitter script.

### 1. Install Rust
```sh
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
```
### 2. Update your PATH
```sh
export PATH="$HOME/.cargo/bin:$PATH"
```
### 3. Reload the shell
```sh
source ~/.bashrc  # If using Bash
source ~/.zshrc   # If using Zsh
```


### 4. Install the repository
```sh
cargo install --git https://github.com/EgorKulikov/submitter
```


## Creating a Bash/Zsh Script for Easy Submission

### 1. Open your shell configuration file

For **Zsh**:
```sh
nano ~/.zshrc
```

For **Bash**:
```sh
nano ~/.bashrc
```

### 2. Add the following function

```sh
cfsubmit() {
  if [ "$#" -ne 2 ]; then
    echo "Usage: cfsubmit <contest_id> <problem_letter>"
    return 1
  fi
  local contest_id="$1"
  local problem_letter="$2"
  local base_url="https://codeforces.com/group/MWSDmqGsZm/contest"
  local url="${base_url}/${contest_id}/problem/${problem_letter}"
  # Set your defaults here:
  local language="C++20"
  local file="solution.cpp"
  submitter "$url" "$language" "$file"
}
```

### 3. Save and exit

Press **CTRL + X**, then **Y**, and hit **Enter**.

### 4. Reload the shell
```sh
source ~/.zshrc  # For Zsh users
source ~/.bashrc  # For Bash users
```

## Usage

Make sure you have your solution file **solution.cpp** in the current directory.  
Then, run the command:

```sh
cfsubmit 219432 D
```

This will submit **solution.cpp** for problem **D** in contest **219432** using **C++20**.

---

### Notes:
- This script assumes that the problem files are named `solution.cpp` by default.
- Make sure **submitter** is installed correctly before running the script.
