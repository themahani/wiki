# Python Version Management with **PyEnv**

Ok, so let's say you want to run a specific python application that requires a different python version than the
one installed on your system. And let's say you don't want to use conda and its variants. Then look no further.
Introducing **PyEnv**! You solution to python version management.

There can be various issues when installing multiple python versions on your system with root access. Including some security concerns.
`pyenv` lets you install any python version you like locally without having to touch the root directory. Everything happens in your own user space.

## Installation

Following the official installation of `pyenv` from their [GitHub repo](https://github.com/pyenv/pyenv), we can use the automatic installer they provide for linux:

```bash
curl -fsSL https://pyenv.run | bash
```

This command will install `pyenv` in your user space.

## Usage

Let's look through some basic use cases.

### Installing Python versions

We can list all the available python version for install by running

```bash
pyenv install -l
```

And then you can install them using

```bash
pyenv install <python-version-of-choice>
```

!!! note
    `pyenv` will choose the latest sub-version if you don't specify the exact version number.
    For example, if I choose `python 3.11`, it will install `python 3.11.13` as the latest exact version number matching your request.

### Switching between Python versions

After we install all the version we need, we can switch between them using various commands. Each with their own scope.

#### Select Python version for current shell only

For this case we can run
```bash
pyenv shell <version>

# For example
pyenv shell 3.11.13
```
And now your shell is using that python version. You can check it by running
```bash
python --version
```
and you can see that the python executable used is from `pyenv` by running
```bash
which python
# Example output:
# /home/user0/.pyenv/shims/python
```
and if you check, you'll see that this python executable is actually a bash script which finds the active python version and executes it

The script would look something like below
```bash
#!/usr/bin/env bash
set -e
[ -n "$PYENV_DEBUG" ] && set -x

program="${0##*/}"

export PYENV_ROOT="/home/ali/.pyenv"
exec "/usr/share/pyenv/libexec/pyenv" exec "$program" "$@"
```
Now I have installed pyenv on my machine system-wide so other users can access it, hence the last line in the script executing the main pyenv executable 
which is located in the root directory.

#### Select Python version for current working directory (and its sub-directories)

This is mainly used when you want to set a python version for your current python project/package.
```bash
pyenv local <version>
```

This will create a `.python-version` plaintext file in your CWD, and write the pyenv python version you chose in it for future reference.
Now anytime you open your terminal in that project (whether the project root dir or any of its sub-dirs), your python version will be set to
the one you specifies.

#### Select Python version for the entire user space

You can achieve this by running
```bash
pyenv global <version>
```
This will write your specified python version to the file `$(pyenv root)/version`. If this file is not available, `pyenv` assumes 
you want to use the system python version.


### Usage with `venv`

Now just having that python version might not be enough. You want to install packages for that specific python version, or create virtual environments
using that python version. This can be done easily.

```bash
# Change directory to your project
cd /path/to/your/python/project

# Set the python version for your project
pyenv local <version>

# Optional, Check to make sure you're using the right version
python --version
# Should ouput <version>

# create virtual environment
python -m venv <venv name>

# Activate the venv
source <venv name>/bin/activate

# Optional, install your desired packages
pip install <your packages>
```
!!! note
    For more info on how to use `venv`, visit [Virtual Environments](venv.md)
