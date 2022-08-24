# New machine configuration

For a long time I've used heavyweight utilities like [prezto](https://github.com/sorin-ionescu/prezto) to configure my development environment, but now that macOS ships with a reasonable install of Zsh by default I've been seeking something more lightweight. This is my current approach. 

#### Install Node/NPM

There are lots of Node version managers, but you're probably best off installing Node with its [official installer](https://nodejs.org/en/download/). Just make sure you configure npm prefix with `npm config set prefix ~/.npm` to avoid needing `sudo` for installs. 

#### Global packages

```bash
npm install --global pure-prompt
```

#### .zshrc

```bash
path+=("/bin")
path+=("/usr/bin")
path+=("/usr/local/bin")
path+=("$HOME/.npm/bin")

# autocomplete
autoload -U compinit; compinit

# change directory without cd
setopt auto_cd

# vs code
path+=("/Applications/Visual\ Studio Code.app/Contents/Resources/app/bin")

# pure prompt
fpath+=("$HOME/.zsh/pure")
autoload -U promptinit; promptinit
prompt pure
```
