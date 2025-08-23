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

Originally inspired from [gelnraya/vscode-settings-json](https://github.com/glennraya/vscode-settings-json.git)

> **NOTE**
> [Backup](#FAQ) your previous configuration (if any exists)

Neovim's configurations are located under the following paths, depending on your OS:

| OS | PATH |
| :- | :--- |
| Linux, MacOS | `$XDG_CONFIG_HOME/nvim`, `~/.config/nvim` |

---
