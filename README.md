ssudoedit - secure sudoedit

sudoedit has a glaring security vulnerability, namely that while editing a
system file X, say a system configuration file and the user executes "write" (:w
in vim, etc. for other editors) the file X will not be modified. 

This is because sudoedit actually modifies a temporary file, and changes are
not synched to the file being synched until the editor is closed. 

This surprising behavior leads developers to avoid sudoedit and instead use
sudo vim, which is very insecure. Thus, sudoedit is insecure because it
forces users to use a different, insecure, tool to do the job.

This repository implements a folklore technique using inotify to sync the temp
file with the file X. It is at least as secure as sudoedit, and has the benefit
that developers actually want to use it.

### Installing

sudo install $PWD/ssudoedit /usr/local/bin/

### Usage

I recommend the following alias in your .bashrc:

```
alias sudoedit='ssudoedit'
```

Reload your bashrc (or open a new terminal), then `sudoedit <file>` to use.
