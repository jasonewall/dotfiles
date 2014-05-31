dotfiles
========

a sub command manager for managing and syncing your bash .files with a git repo

## Usage

First grab the repo

    $ git clone git@github.com:thejayvm/dotfiles
  
All commands are meant to be executed in the repo directory

    $ cd dotfiles
  
Use the `rc` helper to initialize the sub commands

    $ . rc
  
To initialize your dotfiles "install"

    $ dotfiles install dotfiles
  
Then install features that have been included or more likely you have created yourself

    $ dotfiles install <feature>
  
## Features

You can compose you dotfiles as a series of features. For instance, the base repo has a feature for git that:

- Downloads the `git-completion` and `git-prompt.sh` scripts from the github git repo mirror
- Adds a `.bash_profile` source call for each script
- Changes my shell prompt to display the current git branch inside git repos
- Sets my git editor

Features are comprised of the following:

- a sub script in sub/libexec named `dotfiles-<featurename>` (this script should implement at least a blank prep command)
- an entry in dotfiles/dotfiles that looks for and calls, if it exists, the following file
- a file in the dotfiles directory that sets up your env with things related to your feature
- a directory of dotfiles that you want copied to your home directory (not . prefaced, `dotfiles install` will do this for you. This is to keep source control management simpler)
