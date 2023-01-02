dotfiles
========

a sub command manager for managing and syncing your bash .files with a git repo

## Usage

First fork & grab the repo

    $ git clone git@github.com:<yourgithubname>/dotfiles

All commands are meant to be executed in the repo directory

    $ cd dotfiles

Use the `rc` helper to initialize the sub commands

    $ . rc

To initialize your dotfiles "install"

    $ dotfiles install dotfiles

Then install features that have been included or more likely you have created yourself

    $ dotfiles install <feature>

## Features

You can compose your dotfiles as a series of features.

Features are comprised of the following:

- (Optional) a sub script in sub/libexec named `dotfiles-<featurename>` (this script should implement at a prep command; blank if not needed)
- an entry in dotfiles/dotfiles that looks for and calls, if it exists, the following file
- a file in the dotfiles directory that sets up your env with things related to your feature
- a directory of dotfiles that you want copied to your home directory (not . prefaced, `dotfiles install` will do this for you. This is to keep source control management simpler)

E.g. The git feature is comprised of (relative to root of repo)

- File `sub/libexec/dotfiles-git`
    - This has the prep command that downloads the completion scripts
- Directory `git`
    - contains files like my `gitconfig`, and `gitignore_global`
- File `dotfiles/dotfiles-git`
    - File that is copied to ~/.dotfiles and eventually sourced by your .bash_profile

## Contributing

We're all pretty fussy about our dotfiles. They're great because they let us set up our environment in the way that WE want it to work. I wrote this in a way that helps me keep track of what's going on, and hopefully generic enough that other people would find it useful. I also hope that if you add something you will want to share it with others. I want to propose the following to keep the "generic" stuff separate from our "personal" stuff that not everyone might want in their environment.

1. Fork this repo before working with it (you'll have to anyways if you want to keep your features on github)
2. Create a branch to store your personal feature sets and leave `develop` as the generic starting point for other users
3. When you want to add something to the install or update routines, or add things that are generic like uninstall, create a branch off `develop`, and create a pull request to `jasonewall/dotfiles:develop`

## TODO Ideas

- The install command is dependent on ruby. It might be nice to port this into a bash script
- Maybe support zshell? (I've never used zshell so no idea how to go about this)
- Uninstall command
- Move copying of feature file to update so we can separate prep stuff from update stuff
