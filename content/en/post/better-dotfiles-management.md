---
title: "Better Dotfiles Management"
date: 2021-08-14T15:57:06+07:00
draft: false
---

In case you don't know what dotfiles and its purpose is, refer to [this](https://www.freecodecamp.org/news/dive-into-dotfiles-part-1-e4eb1003cff6/).
Dotfiles is a thing that most linux users have and they really put a lot of caring to them. It is really useful when you have to work on multiple environment and just want to get things done quickly. Talking about dotfiles management, there are two main method to manage them: [bare git repos](https://www.atlassian.com/git/tutorials/dotfiles) or simply just [yadm](https://yadm.io/#). These ways are really cumbersome and can easily screwed you up really bad especially when you don't have much experience with GNU/Linux. Luckily, [GNU Stow](https://www.gnu.org/software/stow/) can handle your dotfiles repo easily.

## GNU Stow?
Basically, **GNU Stow** copy existing files from the repo to its **pseudo location** by marking the repo's root as **~**.

Since **Stow** is a GNU package, it is available and even pre-installed on many mainstream GNU/Linux Distributions. Use your own package manager to install the package `stow` in case it isn't present on your machine yet.

## How to construct your own dotfiles?
Assuming you already have `git` and `stow`.

- Create a new directory named **dotfiles** (It must be located on your home directory, I'll explain this later):
```
mkdir -p ~/dotfiles
```
- Now pretending that the **dotfiles** folder is your **~** directory. Move everyfolder and files from the **~** directory to the **dotfiles** directory:
```
cd ~/dotfiles/
mv ~/.zsh* .
mv ~/.config .
mv ~/.vimrc .
mv ~/.xmonad .
mv ~/.gitconfig .
mv ~/.bash* .
and so on...
```

- After moving files and dirs to the dotfiles repo, simply just **stow** it and we're done!
```
cd ~
stow dotfiles
```

Now list the home directory and see the expected result:
```
╭─higanbana@amberbox ~
╰─$ ls ~ | grep "\->"
lrwxrwxrwx   21 higanbana  5 Aug 14:48 .doom.d -> dotfiles/doom/.doom.d
lrwxrwxrwx   23 higanbana  5 Aug 14:48 .xmonad -> dotfiles/xmonad/.xmonad
lrwxrwxrwx   27 higanbana  5 Aug 14:48 .bash_history -> dotfiles/bash/.bash_history
lrwxrwxrwx   26 higanbana  5 Aug 14:48 .bash_logout -> dotfiles/bash/.bash_logout
lrwxrwxrwx   27 higanbana  5 Aug 14:48 .bash_profile -> dotfiles/bash/.bash_profile
lrwxrwxrwx   21 higanbana  5 Aug 14:48 .bashrc -> dotfiles/bash/.bashrc
lrwxrwxrwx   23 higanbana  5 Aug 14:48 .gitconfig -> dotfiles/git/.gitconfig
lrwxrwxrwx   30 higanbana 13 Aug 23:26 .nfdp -> dotfiles/neofetchdisplay/.nfdp
lrwxrwxrwx   20 higanbana  5 Aug 14:48 .zshenv -> dotfiles/zsh/.zshenv
lrwxrwxrwx   19 higanbana  9 Aug 15:36 .zshrc -> dotfiles/zsh/.zshrc
lrwxrwxrwx   33 higanbana  5 Aug 14:48 .zshrc.pre-oh-my-zsh -> dotfiles/zsh/.zshrc.pre-oh-my-zsh
```

