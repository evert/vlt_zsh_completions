# Zsh Completions for vlt

This directory contains the zsh completion script for the [vlt](https://vlt.sh) package manager.

## Installation

There are several ways to install the zsh completion:

### Method 1: Using a completion directory in your `$fpath`

1. Find a directory in your `$fpath`:
   ```bash
   echo $fpath
   ```

2. Copy the `_vlt` file to one of those directories (common locations are `/usr/local/share/zsh/site-functions` or `~/.zsh/completions`):
   ```bash
   # For system-wide installation (may require sudo):
   sudo cp _vlt /usr/local/share/zsh/site-functions/_vlt

   # Or for user-only installation:
   mkdir -p ~/.zsh/completions
   cp _vlt ~/.zsh/completions/_vlt
   ```

3. If you used a custom directory like `~/.zsh/completions`, add it to your `$fpath` in your `~/.zshrc`:
   ```bash
   fpath=(~/.zsh/completions $fpath)
   ```

4. Reload your shell or run:
   ```bash
   autoload -Uz compinit && compinit
   ```

### Method 2: Direct sourcing

Add this to your `~/.zshrc`:
```bash
source /path/to/zsh_completions/_vlt
```

Then reload your shell:
```bash
source ~/.zshrc
```

## Features

The completion script provides:

- **Command completion**: All vlt commands including aliases (e.g., `add`, `i`, `rm`, `u`)
- **Subcommand completion**: For commands like `config`, `cache`, `pkg`, and `token`
- **Global option completion**: All global flags and options with descriptions
- **Command-specific options**: Context-aware options for each command
- **Script completion**: For `vlt run`, it reads your `package.json` to suggest available scripts
- **Directory completion**: For commands that accept directory arguments
- **Value suggestions**: For options like `--view`, `--loglevel`, `--access`, etc.

## Usage Examples

After installation, you can use tab completion with vlt:

```bash
vlt <TAB>                    # Shows all available commands
vlt in<TAB>                  # Completes to "install"
vlt install --<TAB>          # Shows install-specific options
vlt run <TAB>                # Shows available scripts from package.json
vlt config <TAB>             # Shows config subcommands (get, set, delete, list, edit)
vlt --view=<TAB>             # Shows view options (human, json, mermaid, gui)
```

## Troubleshooting

If completions don't work:

1. Make sure the completion system is initialized in your `~/.zshrc`:
   ```bash
   autoload -Uz compinit
   compinit
   ```

2. Check that the `_vlt` file is in your `$fpath`:
   ```bash
   echo $fpath | grep -o '[^ ]*' | while read dir; do [ -f "$dir/_vlt" ] && echo "Found: $dir/_vlt"; done
   ```

3. Clear the completion cache and rebuild:
   ```bash
   rm -f ~/.zcompdump
   compinit
   ```

4. Verify the file has the correct permissions:
   ```bash
   chmod 644 /path/to/_vlt
   ```

## Contributing

If you find any issues or want to add more completion features, please open an issue or pull request at the [vlt repository](https://github.com/vltpkg/vltpkg).
