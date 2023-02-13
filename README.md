# New machine configuration

For a long time I've used heavyweight utilities like [prezto](https://github.com/sorin-ionescu/prezto) to configure my development environment, but now that macOS ships with a reasonable install of Zsh by default I've been seeking something more lightweight. This is my current approach. 

#### Install Node/NPM

There are lots of Node version managers, but you're probably best off installing Node with its [official installer](https://nodejs.org/en/download/). Just make sure you configure npm prefix with `npm config set prefix ~/.npm` to avoid needing `sudo` for installs. 

#### Install deps

```bash
npm install --global pure-prompt
```

```bash
git clone https://github.com/pyenv/pyenv.git ~/.pyenv
pyenv install 3.9 # after sourcing
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

# pyenv
export PYENV_ROOT="$HOME/.pyenv"
command -v pyenv >/dev/null || export PATH="$PYENV_ROOT/bin:$PATH"
eval "$(pyenv init -)"

# pure prompt
fpath+=("$HOME/.zsh/pure")
autoload -U promptinit; promptinit
prompt pure
```

# gCloud CLI
if [ -f '/Users/justinbelcher/google-cloud-sdk/path.zsh.inc' ]; then . '/Users/justinbelcher/google-cloud-sdk/path.zsh.inc'; fi
if [ -f '/Users/justinbelcher/google-cloud-sdk/completion.zsh.inc' ]; then . '/Users/justinbelcher/google-cloud-sdk/completion.zsh.inc'; fi
