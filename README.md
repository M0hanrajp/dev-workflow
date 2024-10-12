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

### Custom VS Code setup:

1. Install "Custom CSS and JS Loader" VS Code Extension.
2. Copy the contents of settings.json to your VS Code's settings.json (warning: it will overwrite your settings).
3. Add vscode_custom_css.imports array to your settings.json file:
```json
"vscode_custom_css.imports": [
    // Absolute file paths for your css/js files
    // For Mac or Linux
    // "file:///Users/your-user-name/custom-vscode.css",
    // "file:///Users/your-user-name/custom-vscode-script.js"

    // For Windows
    // "file:///C:/path-of-custom-css/custom-vscode.css",
    // "file:///C:/path-of-custom-css/custom-vscode-script.js"
],
```
4. You might need to take ownership of the CSS/JS files you made or run VS Code with admin privileges on certain operating system:
5. Enable "Custom CSS and JS Loader" from VS Code's command dialog.
6. Customize the css or js from this repo to make it look the way you want to, or even better, explore areas of VS Code that you want to customize.
7. After making some changes, reload the extension (Reload Custom CSS and JS) from VS Code's command dialog.

Originally inspired from (gelnraya/vscode-settings-json)[https://github.com/glennraya/vscode-settings-json.git]

> **NOTE**
> [Backup](#FAQ) your previous configuration (if any exists)

Neovim's configurations are located under the following paths, depending on your OS:

| OS | PATH |
| :- | :--- |
| Linux, MacOS | `$XDG_CONFIG_HOME/nvim`, `~/.config/nvim` |

---
Thanks :), This is a wip doc.
Upcoming screenshots will be added.
