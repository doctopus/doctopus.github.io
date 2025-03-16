---
title: "Customizing bash zsh oh my zsh"
description: "Customize Bash Terminal"
banner: "/images/sample-blog.jpeg"
tags: ["Linux"]
date: 2023-03-19
---
# OMZ Customizing bash zsh oh my zsh

`echo $0`

Tells which shell you are running.

The configuration files of bash is ~/.bash_profile and that of zsh is ~/zshrc

the configuration file is `~/.zshrc`. In `bash`, it’s `~/.bash_profile`.

Changing shells

Typing bash or zsh switches between them but if you need to set default use the following respective commands for switching to bash and zsh.  `chsh -s $(which bash)` or `chsh -s $(which zsh)` the which bash or which zsh part of the command prints the path to each shells. Alternatively, in the terminal app or iTerm app preferences define the shell opens with from “Default login shell” to "Command" option by writing the path as /bin/bash or /bin/zsh

If you edit the iTerm or terminal settings to define the shell opens in, then it may not be changable from the chsh command.

To add a welcome message while opening a shell edit the respective profiles  `~/.zshrc` or `~/.bash_profile` to add `echo “Welcome to zsh, Human!”`

For bash prompt editing the code in the profile is export PS1=“\u@\h\w $” with the content inside the quotes as per the attributes you want. But for the zshrc the code in the profile is PROMPT='%n:%W:~$'

The (base) in the prompt.
If you have conda installed, it sets `auto_activate_conda: True` and since the base is activated it shows at the prompt. So that means the python in the conda installation gets activated instead of the default python in the system.

To see all conda configuration `conda config - -show` note double dash without space. To see the activation line.

To check this, run:

```other
$ conda config --show | grep auto_activate_base
auto_activate_base: True
```

To set it `False`

```other
conda config --set auto_activate_base False
```

and vice-versa.

Note, if `changeps1` is kept `False`, it will hide `(env)` completely, and in case you want to show `(env)` only when it's activated, you can set `changeps1` to `True`:

```other
conda config --set changeps1 True
```

But the downside is now the shell will use the default python and not the conda python. You may set the auto_activate_base to True to get the conda python activated by default.

To see the status of conda

```shell
conda info | egrep "conda version|active environment"
```

it will show

active environment: None

conda version: 23.1.0

To activate the base environment of conda

`conda activate base`

At this stage now the command prompt will show (base) before the prompt.

To deactivate the conda environment

`conda deactivate`

The need for Oh My Zsh

It is not absolutely needed, it can be considered as a package manager, but it makes it easier to manage the plugins.

Use the command on the website omz.sh to install.

To update use `omz update`, if says omz command not found, use the old commdand `upgrade_oh_my_zsh`

Note: `upgrade_oh_my_zsh` is deprecated. Use `omz update` instead.

The omz directory is at the root .oh-my-zsh 

If you want to uninstall oh-my-zsh , just run uninstall_oh_my_zsh from the command-line. It will remove itself and revert your previous bash or zsh configuration.

## Customizing OMZ
`omz update`  
`omz theme list`  
`omz theme set arrow`  
`omz plugin list`  
`omz plugin enable z`  
`omz plugin info zsh-autosuggestions` [This is not a preinstalled plugin]  
To install the zsh-autosuggestions plugin use the following code to clone the plugin to the custom directory inside .oh-my-zsh from https://github.com/zsh-users/zsh-autosuggestions/blob/master/INSTALL.md

`git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions`

## Install zsh-syntax-highlighting by running:

```
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git $ZSH_CUSTOM/plugins/zsh-syntax-highlighting
```
Note that it should be kept at the end of all plugins in the list of plugins in the .zshrc file.

To change the color of arrow theme, navigate to .oh-my-zsh/themes/arrow.zsh-theme and change the color from the default yellow to green

### Aliases
`alias hpc="ssh 10.88.8.31"`  
 After installing the omz, the configurations in the .bash_profile or .bashrc does not work. All configurations need to be copied to .zshrc 
