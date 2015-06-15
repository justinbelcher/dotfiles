# New machine configuration

#### Install Homebrew and Cask

```bash
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"

brew tap caskroom/cask
brew install brew-cask
```

#### Install latest ZSH
OSX used to ship with a pretty old version of zsh. Yosemite ships with a more recent version of zsh, but you still probably want to install it yourself so you can keep it up to date. In order to choose the homebrew version of zsh as your shell you'll need to add it to the whitelist at `/etc/shells` first. 

```bash
brew install zsh
sudo echo "/usr/local/bin/zsh" >> /etc/shells
chsh -s /usr/local/bin/zsh
```

#### Install Prezto

[Prezto](https://github.com/sorin-ionescu/prezto) is a great configuration framework for zsh, along the lines of `oh-my-zsh` but faster. 
```bash
git clone --recursive https://github.com/sorin-ionescu/prezto.git "${ZDOTDIR:-$HOME}/.zprezto"

setopt EXTENDED_GLOB
for rcfile in "${ZDOTDIR:-$HOME}"/.zprezto/runcoms/^README.md(.N); do
  ln -s "$rcfile" "${ZDOTDIR:-$HOME}/.${rcfile:t}"
done
```

#### Install NVM, Node, and latest NPM

I used to install Node/NPM directly from the Node website, but that requires root and it's tough to run multiple versions of Node and IO in parallel. These days I opt for homebrew versions of Node and NPM managed by [NVM](https://github.com/creationix/nvm). I also go the extra step of storing Node installs in `~/.nvm`, since those binaries are lost when upgrading NVM otherwise. From my experience it's fine to keep NPM up to date even if you're using older versions of node, so I also update it to latest.  

```bash
# install nvm and move nvm-exec to home directory
brew install nvm
mkdir ~/.nvm
cp $(brew --prefix nvm)/nvm-exec ~/.nvm/

# add configuration to prezto profile
echo "export NVM_DIR=~/.nvm" >> ~/.zprofile
echo "source $(brew --prefix nvm)/nvm.sh" >> ~/.zprofile

# install desired version of node
nvm install 0.10
nvm alias default 0.10

# upgrade npm if you want to
npm install -g npm@latest
```

#### Set up my prompt

```bash
npm i -g pure-prompt

# configure prezto to use pure prompt
vim ~/.zpreztorc
:s/theme 'sorin'/theme 'pure'
:wq
```

#### Set up DNS masking for *.dev domains

`dnsmasq` is a convenient way of setting up DNS forwarding for local development. The following is a "set it and forget it" configuration that routes any url ending in `.dev` to localhost.  

```bash
brew install dnsmasq
mkdir -pv $(brew --prefix)/etc/
echo 'address=/.dev/127.0.0.1' > $(brew --prefix)/etc/dnsmasq.conf
sudo cp -v $(brew --prefix dnsmasq)/homebrew.mxcl.dnsmasq.plist /Library/LaunchDaemons
sudo launchctl load -w /Library/LaunchDaemons/homebrew.mxcl.dnsmasq.plist
sudo mkdir -v /etc/resolver
sudo bash -c 'echo "nameserver 127.0.0.1" > /etc/resolver/dev'
```

#### Set up Sublime Text 3

```bash
brew tap caskroom/versions
brew cask install sublime-text3

# install package control (paste following into console & restart)
import urllib.request,os,hashlib; h = 'eb2297e1a458f27d836c04bb0cbaf282' + 'd0e7a3098092775ccb37ca9d6b2e4b7d'; pf = 'Package Control.sublime-package'; ipp = sublime.installed_packages_path(); urllib.request.install_opener( urllib.request.build_opener( urllib.request.ProxyHandler()) ); by = urllib.request.urlopen( 'http://packagecontrol.io/' + pf.replace(' ', '%20')).read(); dh = hashlib.sha256(by).hexdigest(); print('Error validating download (got %s instead of %s), please try manual install' % (dh, h)) if dh != h else open(os.path.join( ipp, pf), 'wb' ).write(by)

# create a package control install manifest
cd ~/Library/Application\ Support/Sublime\ Text\ 3/Packages/User && touch Package\ Control.sublime-settings

# add the following default packages to the Package Control file
# these packages will be automatically installed the next time
# Sublime Text loads up
{
  "installed_packages":
  [
    "Alignment",
    "Babel",
    "EditorConfig",
    "Markdown Preview",
    "Material Theme",
    "SideBarEnhancements",
    "Stylus",
    "SublimeLinter",
    "SublimeLinter-contrib-eslint"
  ]
}
```

At this point replace the default user preferences with the file contained in this repo.

#### Set up iTerm2
```bash
brew cask install iterm2
```

At this point load the iTerm2 settings file contianed in this repo.

#### Set up other standard packages
```bash
brew install git

brew cask install slack
brew cask install rdio
brew cask install dropbox
```

**NOTE:** I used to install chrome via Cask, but it does not play very nice with the App Store version of 1Password (and that version is the only one that works with iCloud syncing). You can still do that if you copy the binary manually to `/Applications`, but these days I think it's simpler to just download the `.dmg` from the website. 
