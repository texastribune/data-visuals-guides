### You and your `.bash_profile`

Your `.bash_profile` is a hidden file that live in your root directory. Your `.bash_profile` is where settings for your terminal belong.

The easiest way to edit your `.bash_profile` with your text editor we installed earlier. In a freshly opened terminal window, run either `subl .bash_profile` or `atom .bash_profile`. (You can always do it with vim – `vim .bash_profile` – too.)

Add this to the top of your `.bash_profile`:

```sh
export PATH=/usr/local/bin:$PATH
```

This tells your terminal to look in `/usr/local/bin` folder for commands you run before hunting for it somewhere else in your `$PATH`. It just so happens that `/usr/local/bin` is where Homebrew installs commands, so this will ensure you are using the Homebrew packages we install. Save this file.

Now you'll need to either open a new terminal window – which will make the `.bash_profile` file load – or `source` it directly. Don't forget to do this every time you make a change!

```sh
source .bash_profile
```
