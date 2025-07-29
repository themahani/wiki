# Virtual Environments

Welcome to package versioning hell :)

Python provides an application known as `venv`, short for _virtual environment_. This
application provide the crucial ability for the user to isolate their Python environment
install thrid-party python packages locally. This is important since installing all of our packages
on the python environment used by the operating system can be very dangerous.

**Why?**:

1. **Root Access**: Installing python packages in the root environment can lead to third-party packages
   gaining root access to your system which can lead to _arbitrary code execution_ on your system.
2. **Clutter**: Working on multiple projects, each requiring a specific set of packages and lead to a large amount of clutter.
3. **Version Conflict**: Some packages depend on specific versions of other packages. This can lead to package version conflicts
   very easily.

## Installation

Your python executable should normally have `venv` preinstalled already.
You can check this by running

```bash
export PHYTON_EXE=$(command -v python || command -v python3)    # depending on you OS the exec name can be either `python` or `python3`
PYTHON_EXE -m venv -h
```

The output should look like below:\

```
usage: venv [-h] [--system-site-packages] [--symlinks | --copies] [--clear] [--upgrade]
            [--without-pip] [--prompt PROMPT] [--upgrade-deps]
            ENV_DIR [ENV_DIR ...]

Creates virtual Python environments in one or more target directories.

positional arguments:
  ENV_DIR               A directory to create the environment in.

options:
  -h, --help            show this help message and exit
  --system-site-packages
                        Give the virtual environment access to the system site-packages
                        dir.
  --symlinks            Try to use symlinks rather than copies, when symlinks are not the
                        default for the platform.
  --copies              Try to use copies rather than symlinks, even when symlinks are the
                        default for the platform.
  --clear               Delete the contents of the environment directory if it already
                        exists, before environment creation.
  --upgrade             Upgrade the environment directory to use this version of Python,
                        assuming Python has been upgraded in-place.
  --without-pip         Skips installing or upgrading pip in the virtual environment (pip
                        is bootstrapped by default)
  --prompt PROMPT       Provides an alternative prompt prefix for this environment.
  --upgrade-deps        Upgrade core dependencies (pip) to the latest version in PyPI

Once an environment has been created, you may wish to activate it, e.g. by sourcing an
activate script in its bin directory.
```

If for any reason you see an `ImportError`, then it means that executable of python doesn't have `venv` installed.\
So let's install it.

### Ubuntu

Using Aptitude (`apt`, `apt-get`), run:

```bash
sudo apt install python3-venv
```

This will install the `venv` package for your system python executable.

### Arch Linux

Using Pacman run:

```bash
sudo pacman -Syy python-venv
```

This command does the same for your Archlinux system.

## Basic Usage

### Creating a new virtual environment

Let's create a new python environment and name it `test`.
Note that I'm assuming the python3 executable name is `python`. In some OS's it can be `python3`.

```bash
python -m venv test
```

Note that this creates the new env in the current directory where the code is executed.
Let's check it for our case:

```bash
pwd
# Example output: /usr/home/user0/
python -m venv test

ls -lh # List cwd in a list with human readable format
# Exampe output:
# total 20K
# drwxr-xr-x  3 user0 user0 4.0K Nov 29  2024 Apps
# drwxr-xr-x 12 user0 user0 4.0K Jul 11 01:14 Code
# drwxr-xr-x  8 user0 user0 4.0K May 24 17:15 dotfiles
# drwx------  5 user0 user0 4.0K Jul 12 12:28 snap
# drwxr-xr-x  5 user0 user0 4.0K Jul 29 12:18 test
```

!!! tip
    You can make choose a custom path using the sample command below:

    ```bash
    python -m venv path/to/your/venv
    ```
