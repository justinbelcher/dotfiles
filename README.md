# IDE: User settings.json
```json
{
    "window.zoomLevel": 0.75,
    "workbench.navigationControl.enabled": false,
    "workbench.layoutControl.enabled": false,
    "window.menuBarVisibility": "compact",
    "workbench.colorTheme": "Framer Syntax",
    "editor.formatOnPaste": true,
    "editor.minimap.enabled": false,
    "editor.fontFamily": "'JetBrainsMono NF', monospace",
    "editor.fontSize": 13,
    "editor.tabSize": 2,
    "terminal.integrated.fontFamily": "'JetBrainsMono NF', monospace",
    "terminal.integrated.fontSize": 13,
}
```

# Brew deps
```bash
brew tap homebrew/cask-fonts
brew install --cask font-jetbrains-mono-nerd-font
brew install jandedobbeleer/oh-my-posh/oh-my-posh
```

# .bashrc
```bash
eval "$(oh-my-posh init bash --config $(brew --prefix oh-my-posh)/themes/hotstick.minimal.omp.json)"
```
