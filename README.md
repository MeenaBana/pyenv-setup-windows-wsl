# pyenv Setup Guide for Windows and WSL
This README provides a comprehensive guide for setting up `pyenv` on a Windows system, configuring specific Python versions as global and local environments, and managing Python versions using Windows Subsystem for Linux (WSL). 

## Table of Contents

1. [Prerequisites](#prerequisites)
2. [Setting Up pyenv on Windows](#setting-up-pyenv-on-windows)
   - [Step 1: Install Prerequisites](#step-1-install-prerequisites)
   - [Step 2: Install pyenv](#step-2-install-pyenv)
   - [Step 3: Set Python Versions](#step-3-set-python-versions)
3. [Setting Up pyenv on WSL](#setting-up-pyenv-on-wsl)
   - [Step 1: Set up a Linux system](#step-1-set-up-a-linux-system)
   - [Step 2: Install pyenv](#step-2-install-pyenv-wsl)
   - [Step 3: Set Python Versions](#step-3-set-python-versions-wsl)
4. [Synchronising Environments Between Windows and WSL](#synchronising-environments-between-windows-and-wsl)
5. [Troubleshooting](#troubleshooting)
6. [References](#references)

## Prerequisites

- A Windows system with administrator access.
- Windows Subsystem for Linux (WSL) installed.

## Setting Up pyenv on Windows

### Step 1: Install Prerequisites

Ensure you have the following installed on your Windows system:

- **Git for Windows**: [Download](https://git-scm.com/download/win) Git for Windows.
   - Run the installer and follow the installation instructions.
   - Ensure that Git is added to your system PATH during the installation process.
- **Python Build Dependencies**:
  - Microsoft Visual C++ Build Tools: [Download Here](https://visualstudio.microsoft.com/visual-cpp-build-tools/)

### Step 2: Install pyenv

1. Open a PowerShell window with Administrator privileges.

2. Install `pyenv` using the `pyenv-win` repository:

   ```powershell
   Invoke-WebRequest -UseBasicParsing https://pyenv.run | Invoke-Expression
   ```

3. Close and reopen the Command Prompt or PowerShell window to apply the changes.

4. With the following command, verify pyenv installation.

```powershell
   pyenv --version
```
### Step 3: Install Python Versions

1. List all available Python versions.

```powershell
pyenv install --list
```
2. Install specific Python versions.

```powershell
pyenv install 3.12.4
pyenv install 3.9.0
```
### Step 4: Set Global or Local Python Version

1. Set a global Python version (This is the default Python version that pyenv will use across the entire system, to all projects and directories unless overridden by a local version).

```powershell
pyenv global 3.12.4
```

2. Set a local Python version for a specific project directory. When set a local Python version, it overrides the global version for that particular directory and its subdirectories.

```powershell
cd path\to\the\project
pyenv local 3.9.0
```

3. Verify the Python version being used.

```powershell
python --version
```

## Setting Up pyenv on WSL

Windows Subsystem for Linux (WSL) can be used to set up a Linux system within a Windows OS.

### Step 1: Set up a Linux system

1. Open PowerShell as Administrator and Enable WSL with command:

```powershell
wsl --install
```
2. After enabling WSL, Ubuntu could be installed as a Linux distribution with command: 

```powershell
wsl --install -d Ubuntu
```
3. Setting WSL Version for better performance.

```powershell
wsl --set-default-version 2
```
4. Once installed, Linux distribution can be launched from the Start menu or by running command:

```powershell
wsl
```

### Step 2: Install pyenv

Inside WSL terminal pyenv can be installed with following commands.

1. Updating package lists

```bash
sudo apt update && sudo apt upgrade -y
```
2. Installing dependencies

```bash
sudo apt install -y make build-essential libssl-dev zlib1g-dev \
libbz2-dev libreadline-dev libsqlite3-dev wget curl llvm \
libncurses5-dev libncursesw5-dev xz-utils tk-dev \
libffi-dev liblzma-dev python-openssl git
```
3. Cloning pyenv repository.

```bash
curl https://pyenv.run | bash
```
4. Adding pyenv to bash so that it loads every time with a new session.

```bash
echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.bashrc
echo 'export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.bashrc
echo 'eval "$(pyenv init --path)"' >> ~/.bashrc
echo 'eval "$(pyenv init -)"' >> ~/.bashrc
```
5. Applying changes.

```bash
source ~/.bashrc
```
6. Verifying pyenv installation.

```bash
pyenv --version
```

### Step 3: Set Python Versions

1. Install specific Python versions for example:

```bash
pyenv install 3.12.4
pyenv install 3.9.0
```
2. Set a global Python version.

```bash
pyenv global 3.12.4
```
3. Set a local Python version.

```bash
cd path\to\the\project
pyenv local 3.9.0
```
