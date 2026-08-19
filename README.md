# Scrabble CLI Solver

A terminal Scrabble solver featuring ANSI table formatting, length filtering, bingo calculations, and dictionary definitions.

## Installation

### Fast Install (POSIX / macOS / Linux)

```sh
curl -fsSL https://raw.githubusercontent.com/danz-the-penguin/scrabble-cli/main/solve -o /usr/local/bin/solve && chmod +x /usr/local/bin/solve
```

## Manual Install

1. Clone the repository
```sh
git clone https://github.com/danz-the-penguin/scrabble-cli.git
cd scrabble-cli
```

2. Make solve executable and place it in your PATH:
```sh
chmod +x solve
sudo mv solve /usr/local/bin/
```

## Usage

### Basic rack solve (? or . for blanks)
```sh
solve "AE?RUI"
```

### Filter by word length
```sh
solve "AETRUI" -l 2       # Only 2-letter words

solve "AETRUI" -l 3-5     # Words between 3 and 5 letters

solve "AETRUI" -l 5+      # 5 letters and longer
```

### Board Constraints
```sh
solve "AETRUI" -s "re"    # Word must start with "re"

solve "AETRUI" -e "ing"   # Word must end with "ing"

solve "AETRUI" -a "z"     # Board anchor tile must be included
```

## Flags
| Flag | Long Flag | Description |
| --- | --- | --- |
| `-s` | `--starts` | Filter words starting with specific letters |
| `-e` | `--ends` | Filter words ending with specific letters |
| `-a` | `--anchor` | Specify board tiles the word must connect through |
| `-l` | `--len` / `--length` | Limit output length (`2`, `3-5`, or `5+`) |
| `-m` | `--middle` | Board letter is strictly in the word

## Completions

### Bash

1. Run this block to create a Bash completion script and append it to your `~/.bashrc`:
```bash
mkdir -p ~/.local/share/bash-completion/completions

cat << 'EOF' > ~/.local/share/bash-completion/completions/solve
_solve_completions() {
    local cur options
    COMPREPLY=()
    cur="${COMP_WORDS[COMP_CWORD]}"
    options="-s --starts -e --ends -m --middle -a --anchor -l --len --length -h --help"

    if [[ ${cur} == -* ]] ; then
        COMPREPLY=( $(compgen -W "${options}" -- ${cur}) )
        return 0
    fi
}
complete -F _solve_completions solve
EOF

# Ensure it loads in ~/.bashrc
grep -qxF 'source ~/.local/share/bash-completion/completions/solve' ~/.bashrc || \
echo 'source ~/.local/share/bash-completion/completions/solve' >> ~/.bashrc
```

2. Reload your profile:
```bash
source ~/.bashrc
```

### Z-shell
1. Run this block to create a Zsh completion definition and enable it in `~/.zshrc`:
```bash
mkdir -p ~/.zsh/completions

cat << 'EOF' > ~/.zsh/completions/_solve
#compdef solve

_solve() {
    _arguments -s \
        '(-s --starts)'{-s,--starts}'[Word must start with these letters]:letters:' \
        '(-e --ends)'{-e,--ends}'[Word must end with these letters]:letters:' \
        '(-m --middle)'{-m,--middle}'[Board letter strictly inside the word]:letters:' \
        '(-a --anchor)'{-a,--anchor}'[Board anchor letters anywhere in word]:letters:' \
        '(-l --len --length)'{-l,--len,--length}'[Filter length (e.g., 5, 2-5, 4+)]:length:' \
        '(-h --help)'{-h,--help}'[Show help message]' \
        '1:rack letters:'
}

_solve "$@"
EOF

# Append fpath setup to ~/.zshrc if not already present
grep -qxF 'fpath=(~/.zsh/completions $fpath)' ~/.zshrc || echo 'fpath=(~/.zsh/completions $fpath)' >> ~/.zshrc
grep -qxF 'autoload -U compinit && compinit' ~/.zshrc || echo 'autoload -U compinit && compinit' >> ~/.zshrc
```
2. Reload your profile:
```bash
source ~/.zshrc
```


## Roadmap & Future Updates

- [x] ANSI color-coded table output
- [x] Length filtering (`-l` / `--len`)
- [ ] Definitions
- [ ] Custom dictionary file support (`--dict`)
- [ ] Multi-language support

## Credits & Acknowledgements

Special thanks to the creators and maintainers of the word lists and dictionary datasets that power this tool:

* **Scrabble Word List**: Official tournament word list hosted by [raun/Scrabble](https://github.com/raun/Scrabble).
* **Definitions Database**: Powered by open-source English definitions (Webster's Unabridged Dictionary dataset) hosted by
  [matthewreagan/WebstersEnglishDictionary](https://github.com/matthewreagan/WebstersEnglishDictionary)
* **Fallback Word List**: Native Unix system dictionary (`/usr/share/dict/words`).

