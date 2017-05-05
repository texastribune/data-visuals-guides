# Installing Python

The first Homebrew package we're going to install is Python. "But wait," you say, "my computer already has Python!"

You're right! But it's a good idea to not monkey around with your computer's installed software. There's some fragile stuff in there that your computer depends on to function, so we try our best not to disturb it. Plus it is much easier to troubleshoot if you know exactly where your version of Python lives.

Homebrew has [dedicated an entire document](https://github.com/Homebrew/homebrew/blob/master/share/doc/homebrew/Homebrew-and-Python.md) to how it works with Python. It's worth a quick read.

The Data Visuals team defaults to **Python 3**. So we'll install both Python 2 and 3.

```sh
brew install python
pip install --upgrade setuptools pip
pip install --upgrade

brew install python3
pip3 install --upgrade setuptools pip wheel