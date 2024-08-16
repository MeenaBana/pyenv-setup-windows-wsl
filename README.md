# pyenv Setup Guide for Windows and WSL
This README provides a comprehensive guide for setting up `pyenv` on a windows system, configuring specific python versions as global and local environments, and managing python versions using Windows Subsystem for Linux (WSL). 

## Table of Contents

1. [Prerequisites](#prerequisites)
2. [Setting up pyenv on windows](#setting-up-pyenv-on-windows)
   - [Step 1: Install prerequisites](#step-1-install-prerequisites)
   - [Step 2: Install pyenv](#step-2-install-pyenv)
   - [Step 3: Install python versions](#step-3-install-python-versions)
   - [Step 4: Set global and local python version](#step-4-set-global-and-local-python-version)
3. [Setting up pyenv on wsl](#setting-up-pyenv-on-wsl)
   - [Step 1: Set up Linux system](#step-1-set-up-a-linux-system)
   - [Step 2: Install pyenv wsl](#step-2-install-pyenv-wsl)
   - [Step 3: Set python versions](#step-3-set-python-versions)

## Prerequisites

- A Windows system with administrator access.
- Windows Subsystem for Linux (WSL) installed.

## Setting Up pyenv on windows

### Step 1: Install prerequisites

Ensure the following installations on the Windows system:

- **Git for Windows**: [Download](https://git-scm.com/download/win) Git for Windows.
   - Run the installer and follow the installation instructions.
   - Ensure that git is added to the system PATH during the installation process.
- **Python Build Dependencies**:
  - [Download](https://visualstudio.microsoft.com/visual-cpp-build-tools/) Microsoft Visual C++ Build Tools.

### Step 2: Install pyenv

1. Open a PowerShell window with administrator privileges.

2. Install `pyenv` using the `pyenv-win` repository:

   ```powershell
   Invoke-WebRequest -UseBasicParsing https://pyenv.run | Invoke-Expression
   ```

3. Close and reopen the PowerShell window to apply the changes.

4. With the following command, verify pyenv installation.

```powershell
   pyenv --version
```
### Step 3: Install python versions

1. List all available Python versions.

```powershell
pyenv install --list
```
2. Install specific python versions.

```powershell
pyenv install 3.12.4
pyenv install 3.9.0
```
### Step 4: Set global and local python version

1. Set a global python version (this is the default python version that pyenv will use across the entire system, to all projects and directories unless overridden by a local version).

```powershell
pyenv global 3.12.4
```

2. Set a local python version for a specific project directory. When set a local python version, it overrides the global version for that particular directory and its subdirectories.

```powershell
cd path\to\the\project
pyenv local 3.9.0
```

3. Verify the python version being used.

```powershell
python --version
```

## Setting up pyenv on wsl

Windows Subsystem for Linux (WSL) can be used to set up a Linux system within a Windows OS.

### Step 1: Set up Linux system

1. Open PowerShell as administrator and enable wsl with command:

```powershell
wsl --install
```
2. After enabling wsl, ubuntu could be installed as a Linux distribution with command: 

```powershell
wsl --install -d Ubuntu
```
3. Setting wsl version for better performance.

```powershell
wsl --set-default-version 2
```
4. Once installed, Linux distribution can be launched from the start menu or by running command:

```powershell
wsl
```

### Step 2: Install pyenv wsl

Inside wsl terminal pyenv can be installed with following commands.

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

### Step 3: Set python versions

1. Install specific python versions for example:

```bash
pyenv install 3.12.4
pyenv install 3.9.0
```
2. Set a global python version.

```bash
pyenv global 3.12.4
```
3. Set a local python version.

```bash
cd path\to\the\project
pyenv local 3.9.0
```
