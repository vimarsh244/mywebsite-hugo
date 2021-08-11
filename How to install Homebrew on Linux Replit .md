# How to install Homebrew on Linux Replit 
 ```
 mkdir homebrew && curl -L https://github.com/Homebrew/brew/tarball/master | tar xz --strip 1 -C homebrew

export PATH="$(pwd)/homebrew/bin:$PATH" && brew

```
Note: run export PATH="$(pwd)/homebrew/bin:$PATH" whenever you want to use something.

https://replit.com/talk/learn/Homebrew/116107

# install homebrew on github codespaces

```
sudo apt-get install build-essential procps curl file git

/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

```

edit from github codespaces