# 🎨 Developer workflow setup

Welcome to my configuration repository! Here, you'll find my personal setups for **Neovim** (`init.lua`) and **Windows Terminal** (`settings.json`). Feel free to explore and use these files to fine-tune your own configurations. Enjoy customizing your environment!

Let me know if there's anything else you'd like to add or modify!

## 🚀 Getting Started

### My personal Neovim setup 

You can download the latest release from the [Neovim GitHub releases page](https://github.com/neovim/neovim/releases/tag/stable). Here are the steps to do so:

### For Linux

1. **Download the AppImage:**
   ```bash
   curl -LO https://github.com/neovim/neovim/releases/download/stable/nvim.appimage
   ```
2. **Make it executable:**
   ```bash
   chmod u+x nvim.appimage
   ```
3. **Extract the AppImage:**
   ```bash
   ./nvim.appimage --appimage-extract
   ```
4. **Run Neovim:**
   ```bash
   ./squashfs-root/AppRun
   ```
### Create a Symbolic Link

To run Neovim using the `nvim` command, you can create a symbolic link:

1. **Move the extracted directory to a suitable location:**
   ```bash
   sudo mv squashfs-root /opt/nvim
   ```
2. **Create a symbolic link:**
   ```bash
   sudo ln -s /opt/nvim/AppRun /usr/bin/nvim
   ```
3. **Verify the installation:**
   ```bash
   nvim --version
   ```
### Clone kickstart.nvim   
   
Please refer [kickstart.nvim](https://github.com/nvim-lua/kickstart.nvim) for more information.

### Install External Dependencies

External Requirements:
- Basic utils: `git`, `make`, `unzip`, C Compiler (`gcc`)
- [ripgrep](https://github.com/BurntSushi/ripgrep#installation)
- Clipboard tool (xclip/xsel/win32yank or other depending on platform)
- A [Nerd Font](https://www.nerdfonts.com/): optional, provides various icons
  - if you have it set `vim.g.have_nerd_font` in `init.lua` to true
- Language Setup:
  - If want to write Typescript, you need `npm`
  - If want to write Golang, you will need `go`
  - etc.

### Install Kickstart
```sh
git clone https://github.com/nvim-lua/kickstart.nvim.git "${XDG_CONFIG_HOME:-$HOME/.config}"/nvim
```

### Post Installation

Start Neovim

```sh
nvim
```

That's it! Lazy will install all the plugins you have. Use `:Lazy` to view current plugin status. Hit `q` to close the window.

Read through the `init.lua` file in your configuration folder for more information about extending and exploring Neovim. That also includes examples of adding popularly requested plugins.

Here's a youtube tutorial : [The Only Video You Need to Get Started with Neovim](https://www.youtube.com/watch?v=m8C0Cq9Uv9o)

> **NOTE**
> [Backup](#FAQ) your previous configuration (if any exists)

Neovim's configurations are located under the following paths, depending on your OS:

| OS | PATH |
| :- | :--- |
| Linux, MacOS | `$XDG_CONFIG_HOME/nvim`, `~/.config/nvim` |

---

Thanks :)
 
## 🛠️ Configurations

Here's a brief overview of the configurations you'll find in this repository:

- **Editor Configs:**
  - VSCode
  - Sublime Text
  - Vim

- **Shell Configs:**
  - Bash
  - Zsh
  - Fish

- **Development Environment:**
  - Docker
  - Kubernetes
  - Virtual Environments

- **Miscellaneous:**
  - Git
  - Tmux
  - Custom Scripts
