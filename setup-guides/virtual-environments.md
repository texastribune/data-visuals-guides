### Virtual environments

When you start working on group projects, it's important to make sure that everyone's working environment is as close to identical as possible. Virtual environments keep a Python project's installs in their own little boxes so there are no conflicts between versions being used in other projects, or those already installed on your computer.

#### Installing `virtualenv` and `virtualenvwrapper`

Run this command in your terminal:

```sh
pip3 install virtualenvwrapper
```

To look at a list of what's currently installed in your environment, you can run the following:

```sh
pip3 freeze
```

Now we need to use our `.bash_profile` to set some settings for `virtualenv`.
Open your `.bash_profile` and add these lines:

```sh
export WORKON_HOME=$HOME/.virtualenvs
export VIRTUALENVWRAPPER_PYTHON=$(which python3)
source /usr/local/bin/virtualenvwrapper.sh
```

Save, then `source` your `.bash_profile`.

#### Creating a virtual environment

Virtual environments are created with the `mkvirtualenv` command.

Try it out!

```sh
mkvirtualenv test
```

This will create a Python 3 environment. You'll get some feedback as it installs `pip`, then your new terminal prompt should begin with `(test)`.

To turn off your environment, run `deactivate`.

Great job! You did it!

> HEADS UP! Make sure you **are not in a virtual environment** when installing packages with Homebrew. Things could get weird. Always `deactivate` before any `brew install` commands.

#### But I need Python 2!

The way we set up `virtualenvwrapper` defaults to using Python 3 in the environment. But it is still possible to create Python 2 environments.

```sh
mkvirtualenv --python `which python` <name-of-environment>
```

The ``--python `which python` `` tells `mkvirtualenv` to use regular `python` to create the environment. In our case, that is referencing our Python 2 instance we installed earlier with Homebrew.