# Signing commits with GPG
---

This document is a simple step by step guideline on how to create a GPG key and use this to sign Git commits with.

Tested with:
| OS      | Tool               | Platform |
|---------|--------------------|----------|
| Windows | CLI                | Github   |
| Windows | Visual Studio      | Github   |
| Windows | Visual Studio Code | Github   |
| Windows | Smartgit           | Github   |
| MacOS   | CLI                | Github   |
| MacOS   | Smartgit           | Github   |
| MacOS   | Visual Studio Code | Github   |

---

## Generating keys
### Windows
#### Step 1: Download GnuPG
First of all, download and install [GnuGP](https://gnupg.org/download/).
A Windows installer is available.

#### Step 2: Generate key
Open a command shell and execute the following command:
```
gpg --gen-key
```

#### Step 3: Check & copy key
GnuPG comes with Kleopatra.
Either open Kleopatra, or open the file `C:\Users\{user}\AppData\Roaming\gnupg\trustdb.gpg` (with Kleopatra).

The key should be available:
![Kleopatra](img/01.Kleopatra.png)

Now double click the key and choose export.
Copy all the text in the window and use this to add this public key to a (git) platform like Github.
See the chapter `Adding keys to a platform` in this Readme file.
![Kleopatra key export](img/02.Kleopatra-export.png)

#### Step 4: Set signing with GPG key for commits in Git global settings
Now open the (global) .gitconfig file, usually `C:\Users\{user}\.gitconfig`.

Add `gpgsign = true` under `[commit]`.
Add `program = {gpg.exe-full-location}` under `[commit]`.

An example of this file:

```
[user]
	name = Jordi Jolink
	email = mail@jordijolink.nl
[commit]
	gpgsign = true
[gpg]
	program = C:\\Program Files (x86)\\gnupg\\bin\\gpg.exe
```

Validate the settings by opening a command shell and executing the following command: `git config -l`.
This will list all of the settings, and should include the `gpgsign` and `program` setting.

Example output:
![git config -l](img/03.GitConfigList.png)

### MacOS
#### Step 1: Download GnuPG
First, install GPG.
Open a terminal and execute the following commands:
```
brew install gpg
brew cask install gpg-suite
```

Next, you should add a line to your profile file.
This can be either of these files:
* ~/.profile
* ~/.bash_profile
* ~/.zshrc

In this example the (currently) newest shell (zsh) is used.
Execute the following command in the terminal to open the profile:
```
nano ~/.zshrc
```

Add the following line, save (CTRL+O), quit (CTRL+X) and completely close the terminal (CMD+Q).
```
export GPG_TTY=$(tty)
```

#### Step 2: Generate key
Open a terminal and execute the following command:
```
gpg --gen-key
```

#### Step 3: Export & copy key
In a terminal, execute the following command to get an overview of your keys:
```
gpg --list-keys
```

The email address of the key listed, must be used in the next command:
```
gpg --armor --export {emailaddress}
```

Copy all the text in the window and use this to add this public key to a (git) platform like Github.
See the chapter `Adding keys to a platform` in this Readme file.

#### Step 4: Set signing with GPG key for commits in Git global settings
Run the following command in the terminal to add signing to the global git configuration:
```
git config --global commit.gpgsign true
git config --global gpg.program /usr/local/MacGPG2/bin/gpg2
```

Validate the settings by opening a terminal and executing the following command: `git config -l`.
This will list all of the settings, and should include the `gpgsign` setting.
Also, the `email` setting should be the same as your key's.

---

## Adding keys to a platform
### Github
For this, the contents of the public key must be copied to the clipboard.
Go to Github, click you profile icon, go to settings and open `SSH and GPG keys`.
On the bottom of the page click the button `New GPG key`.
Paste the GPG key and add it.

### Azure DevOps
_Will be added in the future._
