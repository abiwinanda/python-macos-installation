# Installing and Managing Python on macOS

Python installations can be a mess, especially on macOS, because of multiple overlapping sources (system Python, Homebrew, pyenv, conda, official installer, etc). This guide serves as a reminder to the original author (or anyone) for how to install Python in macOS the recommended way.

## 1. Checking Existing Python Installation

Before installing a new version of Python, check if it is already installed:

```sh
python3 --version
which python3
```

Common outputs:

- `/usr/bin/python3` → Apple's system Python (not recommended for development).
- `/opt/homebrew/bin/python3` or `/usr/local/bin/python3` → Homebrew Python.
- `/Library/Frameworks/Python.framework/Versions/X/bin/python3` → Installed via the official Python installer.

To see if Python is installed via Homebrew:

```sh
brew list | grep python
```

## 2. Recommended Installation Method: Homebrew

Using Homebrew is the easiest and most flexible way to install Python.

### **Install Homebrew (if not already installed):**

```sh
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

Verify Homebrew installation:

```sh
brew --version
```

### **Install Python via Homebrew:**

```sh
brew install python
```

Check the installed version:

```sh
python3 --version
```

### **Upgrade Python via Homebrew:**

```sh
brew update
brew upgrade python
```

### **Ensure Homebrew Python is Used:**

If `python3` still points to an older version (installed not through homebrew), force Homebrew to take priority:

```sh
brew link --overwrite python
```

If that doesn't work, restart your terminal or run:

```sh
exec zsh
hash -r
```

## 3. Alternative Installation: Official Python Installer

If you prefer to install Python without Homebrew, download it from [python.org](https://www.python.org/downloads/macos/).

- Install the `.pkg` file and follow the instructions.
- Verify installation with `python3 --version`.
- If needed, add Python to your `$PATH`:
  ```sh
  export PATH="/Library/Frameworks/Python.framework/Versions/Current/bin:$PATH"
  ```

## 4. Managing Multiple Python Versions

If you need multiple Python versions, use `pyenv`:

```sh
brew install pyenv
pyenv install 3.12.3  # Example version
pyenv global 3.12.3
```

Check the active version:

```sh
pyenv version
```

## 5. Uninstalling Python

### **Uninstall Homebrew Python:**

```sh
brew uninstall python
brew cleanup
```

### **Uninstall Python Installed from Official Installer:**

```sh
sudo rm -rf /Library/Frameworks/Python.framework
sudo rm -rf /usr/local/bin/python3
```

## 6. Best Practices

- **Use Homebrew** if you need frequent updates and package management.
- **Use pyenv** if you work with multiple Python versions.
- **Avoid modifying macOS system Python** (`/usr/bin/python3`).
- **Alias python3 to python** for ease of typing.

Now you're ready to use Python effectively on macOS! 🚀
