## Installing git

> You'll need a [GitHub](http://github.com/) account and be a member of the Texas Tribune organization. Someone should help you get this set up – don't worry!

To get this started, install git:

```sh
brew install git
```

Now we need to set some defaults for the git client. First we need to your name for commits.

> This should not be your GitHub user account name. It's meant to be your real name – like Jenny Smith – but you are not required to do so. This name will be public and attached to every one of your commits. Feel free to use a pseudonym!

To set your name, run the following:

```sh
git config --global user.name "<your-name>"
```

Next we'll set your email. This needs to be an email account associated with your Github account. Like the name, this email will be publically available and attached to each of your commits. If you don't know which emails are under your GitHub account, you can [check on GitHub](https://github.com/settings/emails).

```sh
git config --global user.email "<your-email>"
```

> Don't want your email public? GitHub can help with that. On the email settings page, there is a setting at the bottom labeled `Keep my email address private`. You can then use the proxy email GitHub provides.

Next we'll set up authentication. The Homebrew install of git adds a helper that allows it to use OSX's built-in Keychain.

Run the following to tell git to use it:

```sh
git config --global credential.helper osxkeychain
```

We also need to tell git to use `https` for cloning.

```sh
git config --global hub.protocol https
```

###BONUS!
## Hub

`hub` is an extension for git that adds extra functionality. [Read more about the perks](https://hub.github.com/).

To install, we'll use Homebrew:

```sh
brew install hub
```

Next, we'll need to alias `hub` to point to git in your `.bash_profile`. (Don't forget to `source`!)

```sh
alias git=hub
```
