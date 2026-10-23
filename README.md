# Dotfiles

Personal configuration for Zsh, Vim, Vifm, and Hyprland. The Vim configuration uses the Rosé Pine theme.

## Requirements on Arch Linux

Install the tools needed for the Zsh and Vim configurations:

```sh
sudo pacman -Syu
sudo pacman -S zsh vim git curl
```

The Vim configuration uses `vim-plug` to install its plugins. Its Vim-Go plugin also runs `GoUpdateBinaries` when installed, and Go files are configured to use `gopls` and `goimports`. Install the Go tools before installing Vim plugins:

```sh
sudo pacman -S go gopls go-tools
```

`go-tools` provides `goimports` on Arch. If you only want the editor theme and do not need Go support, you can omit the Go tools, but the Vim-Go plugin's post-install command may not complete.

Install the go plugins:
```sh
go install golang.org/x/tools/gopls@latest
go install golang.org/x/tools/cmd/goimports@latest
```

## Install the Rosé Pine setup

Clone the repository:

```sh
git clone https://github.com/LewisLint/dotfiles.git ~/.dotfiles
cd ~/.dotfiles
```

Back up any existing files and install the Rosé Pine configs:

```sh
cp --backup=numbered rose/.zshrc ~/.zshrc
cp --backup=numbered rose/.vimrc ~/.vimrc
```

GNU `cp` creates numbered backups if those files already exist. The files at the repository root (`.zshrc` and `.vimrc`) are an alternative copy; currently, they are identical to the files in `rose/`. Choose either pair rather than installing both.

Install `vim-plug`, then install the Vim plugins:

```sh
curl -fLo ~/.vim/autoload/plug.vim --create-dirs \
  https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim
vim +PlugInstall +qall
```
Alternatively, if you have the AUR avaliable (which you almost certainlly do on Arch),  you can just install `vim-plug` with yay:
```sh
yay -S vim-plug
```
The Rosé Pine Vim theme is installed by `vim-plug`. Open Vim to use it. The Zsh config is active in new shells; to make Zsh your login shell, run:

```sh
chsh -s "$(command -v zsh)"
```

Log out and back in for the login-shell change to take effect.

## Other configurations

These files are optional; install only the ones you use.

### Vifm

The Vifm config opens a Zsh terminal pane, launches Neovim for file editing, and selects the `onedark` color scheme from Vifm-Colors. Install the dependencies and theme:

```sh
sudo pacman -S vifm neovim zsh
mkdir -p ~/.config/vifm
git clone https://github.com/vifm/vifm-colors.git ~/.config/vifm/colors
```

Then back up and install the config:

```sh
cp --backup=numbered vifm.conf ~/.config/vifm/vifmrc
```

### Hyprland

`hyprland.conf` is an optional, machine-specific configuration. It references applications, a cursor theme, wallpaper locations, and absolute paths that may not exist on another system. Review and edit those references before installing it; do not replace an existing Hyprland config without backing it up.

## Optional Zsh aliases

The Zsh config includes aliases that need extra applications:

- `img` and `ig` use Ristretto.
- `ytdlp` uses `yt-dlp` and Chromium to access browser cookies.

Install them only if you want those aliases:

```sh
sudo pacman -S ristretto yt-dlp chromium
```
