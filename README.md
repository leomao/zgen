## zgen

A lightweight plugin manager for ZSH inspired by Antigen. The goal is to have a minimal overhead when starting up the shell because nobody likes waiting. The script does nothing but sources your plugins and appends them to fpath.

### Usage

#### Load oh-my-zsh base
    zgen oh-my-zsh

#### Load oh-my-zsh plugins
    zgen oh-my-zsh <location>
This is a shortcut for `zgen load`.

#### Or if you prefer prezto
    zgen prezto
This will also create a symlink in the ZSHDOT or HOME directory. This is needed by prezto

#### Load prezto plugins
    zgen prezto <modulename>
This is uses the prezto method for loading modules

#### Load a repo as prezto plugins
    zgen pmodule <reponame> <branch>
This is uses the prezto method for loading the module, by creating a symlink and calling pmodule

#### Set prezto options
    zgen prezto <modulename> <option> <value(s)>
This must be used before the module is loaded. Or if the default modules should be loaded (default) these settings must be done before the `zgen prezto` command. `module` is prepended if the name does not start with `module`, `prezto` or a `*`, `prezto` is prepended if it does not start with `prezto`.

#### Load plugins and completions
    zgen load <repo> [location] [branch]
Similar to `antigen bundle`. It tries to source any scripts from `location`. If none found, it adds `location` to `$fpath`.

- `repo`
    - github 'user/repository' or path to a local repository
- `location`
    - relative path to a script/folder
    - useful for repositories that don't have proper plugin support like `zsh-users/zsh-completions`
- `branch`
    - for those who don't use the master branch

#### Update zgen framework
    zgen selfupdate

#### Update all repositories and remove the init script
    zgen update

### Example .zshrc

```zsh
# load zgen
source "${HOME}/proj/zgen/zgen.zsh"

zgen oh-my-zsh

# plugins
zgen oh-my-zsh plugins/git
zgen oh-my-zsh plugins/sudo
zgen oh-my-zsh plugins/command-not-found
zgen load zsh-users/zsh-syntax-highlighting
zgen load /path/to/super-secret-private-plugin

# bulk load
zgen loadall <<EOPLUGINS
    zsh-users/zsh-history-substring-search
    /path/to/local/plugin
EOPLUGINS
# ^ can't indent this EOPLUGINS

# completions
zgen load zsh-users/zsh-completions src

# theme
zgen oh-my-zsh themes/arrow

```

### Example .zshrc for prezto use
Here is a partial example how to work with prezto

```zsh
...
    echo "Creating a zgen save"

    # prezto options
	zgen prezto editor key-bindings 'emacs'
	zgen prezto prompt theme 'sorin'

    # prezto and modules
    zgen prezto
    zgen prezto git
    zgen prezto command-not-found
    zgen prezto syntax-highlighting

    # plugins
    zgen load /path/to/super-secret-private-plugin
....

```

## Other resources

The [awesome-zsh-plugins](https://github.com/unixorn/awesome-zsh-plugins) list contains many zgen-compatible zsh plugins & themes that you may find useful.
