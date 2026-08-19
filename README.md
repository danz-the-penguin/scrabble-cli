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

   

