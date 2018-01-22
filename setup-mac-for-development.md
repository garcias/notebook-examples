## Command line tools

Install the command line tools. 
Run the script below on the Terminal, and click **Install** when prompted by system dialog (not **Get Xcode**). 
This script *does not* download the enormous IDE, though it does download a lot (~130 MB). 
The process takes about 10 minutes.

```bash
xcode-select --install
# xcode-select: note: install requested for command line developer tools
```

## Homebrew

Install Homebrew for package management, by downloading and running a Ruby script from Homebrew's GitHub repo. Press **RETURN** and authenticate. The command below uses Curl to download the Hombrew install script and then tells Ruby to execute the result. 

```bash
usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
# ==> This script will install:
# /usr/local/bin/brew
# /usr/local/share/doc/homebrew
# ...
# Press RETURN to continue or any other key to abort
```

When installation is complete, the following message will print to the terminal.

```bash
# ==> Installation successful!
# 
# ==> Homebrew has enabled anonymous aggregate user behaviour analytics.
# Read the analytics documentation (and how to opt-out) here:
#   https://docs.brew.sh/Analytics.html
# 
# ==> Next steps:
# - Run `brew help` to get started
# - Further documentation: 
#     https://docs.brew.sh
```

To ensure that Homebrew's version of tools take precedence, make sure `/usr/local/bin` is first in the `PATH` variable in `.bash_profile`.

```bash
echo 'export PATH="/usr/local/bin:$PATH"' >> ~/.bash_profile
```

### Test Homebrew

Homebrew apparently expects to manage just about everything in `/usr/local/lib`. To see if there are conflicting versions of libraries, run `brew doctor`.

```bash
brew doctor
# Warning: Unbrewed dylibs were found in /usr/local/lib.
# If you didn't put them there on purpose they could cause problems when
# building Homebrew formulae, and may need to be deleted.
# 
# Unexpected dylibs:
#   /usr/local/lib/libtcl8.6.dylib
#   /usr/local/lib/libtk8.6.dylib
```

These came from Anaconda and R. I only use those on VMs now, so I removed all the files that Homebrew cited.

```bash
cd /usr/local/lib
ls *.dylib
# libtcl8.6.dylib libtk8.6.dylib
rm -f *.dylib

rm -f ../include/*.h
rm -f pkgcontrol/*.pc
rm -f *.a
# Pruned 1 symbolic links and 1 directories from /usr/local
```

Update the package listing.

```bash
brew update
# Updated 1 tap (homebrew/core).
# ==> New Formulae
# node@8
# ==> Updated Formulae
# abcmidi                   flow                      jruby                    
# clojure                   fn                        kontena                  
# fibjs                     heimdal                   liblinear                
# libmicrohttpd             node-build                presto
# mrboom                    node@4                    telegraf
# node                      node@6                    tmuxinator-completion
```

## Git

Use Homebrew to install the latest Git. Then configure it.

```bash
brew install git
# ==> Downloading https://homebrew.bintray.com/bottles/git-2.15.1.sierra.bottle.tar.gz
# ######################################################################## 100.0%
# ==> Pouring git-2.15.1.sierra.bottle.tar.gz
# ==> Caveats
# Bash completion has been installed to:
#   /usr/local/etc/bash_completion.d
# 
# zsh completions and functions have been installed to:
#   /usr/local/share/zsh/site-functions
# 
# Emacs Lisp files have been installed to:
#   /usr/local/share/emacs/site-lisp/git
# ==> Summary
# 🍺  /usr/local/Cellar/git/2.15.1: 1,488 files, 34.1MB
```

Then configure Git. Skip the last line if using SSH with pubic-key encryption.

```bash
git config --global user.name "Simon Garcia"
git config --global user.email "garcias@users.noreply.github.com"
git config --global color.ui auto
git config --global core.excludesfile "~/.gitignore_global"
git config --global credential.helper osxkeychain # if using HTTPS without 2FA for pushing
```

Make sure `.gitignore_global` contains patterns appropriate for macOS

```bash
.DS_Store
.DS_Store?
._*
.Spotlight-V100
.Trashes
ehthumbs.db
Thumbs.db
*.pyc
*.out
venv
.vagrant
```

## Keys

Generate a key pair (4096-bit RSA) for SSH access to GitHub. Start the SSH agent and add the key to it. Copy the public key to the macOS system clipboard and register it with GitHub. It should begin with `ssh-rsa` and end with the comment text (e.g. `garcias@kenyon.edu`).

```bash
ssh-keygen -t rsa -b 4096 -C "garcias@kenyon.edu" -f id_rsa
eval "$(ssh-agent -s)"
ssh-add -K ~/.ssh/id_rsa
cat ~/.ssh/id_rsa.pub | pbcopy
```

