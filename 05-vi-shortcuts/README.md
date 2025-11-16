# ⌨️ Vi/Vim Shortcuts - Quick Reference

> Essential keyboard shortcuts for Vi/Vim text editor

---

## 📑 Table of Contents

| Section | Description |
|---------|-------------|
| [Modes](#modes) | Understanding Vi modes |
| [Starting & Quitting](#starting--quitting) | Open and close files |
| [Navigation](#navigation) | Move around |
| [Editing](#editing) | Insert and modify text |
| [Deleting](#deleting) | Remove text |
| [Copy & Paste](#copy--paste) | Clipboard operations |
| [Search & Replace](#search--replace) | Find and replace |
| [Saving](#saving) | Save files |

---

## Modes

### Vi Modes

| Mode | How to Enter | Purpose |
|------|--------------|---------|
| **Normal** | `Esc` | Navigate and run commands (default) |
| **Insert** | `i`, `a`, `o` | Type text |
| **Visual** | `v`, `V` | Select text |
| **Command** | `:` | Execute commands |

---

## Starting & Quitting

### Opening Files

| Command | Description |
|---------|-------------|
| `vi filename` | Open file |
| `vi +10 filename` | Open at line 10 |
| `view filename` | Open read-only |

### Exiting

| Command | Description |
|---------|-------------|
| `:q` | Quit (if no changes) |
| `:q!` | Quit without saving |
| `:wq` | Save and quit |
| `:x` | Save (if changed) and quit |
| `ZZ` | Save and quit (shortcut) |
| `ZQ` | Quit without saving (shortcut) |

---

## Navigation

### Basic Movement

| Key | Action |
|-----|--------|
| `h` | Left |
| `j` | Down |
| `k` | Up |
| `l` | Right |

### Word Movement

| Key | Action |
|-----|--------|
| `w` | Next word start |
| `b` | Previous word start |
| `e` | Next word end |

### Line Movement

| Key | Action |
|-----|--------|
| `0` | Start of line |
| `^` | First non-blank character |
| `$` | End of line |

### Page Movement

| Key | Action |
|-----|--------|
| `gg` | First line of file |
| `G` | Last line of file |
| `10G` | Go to line 10 |
| `Ctrl+f` | Page down |
| `Ctrl+b` | Page up |
| `Ctrl+d` | Half page down |
| `Ctrl+u` | Half page up |

### Search Navigation

| Key | Action |
|-----|--------|
| `/text` | Search forward for "text" |
| `?text` | Search backward for "text" |
| `n` | Next search result |
| `N` | Previous search result |
| `*` | Search word under cursor |

---

## Editing

### Insert Mode

| Key | Action |
|-----|--------|
| `i` | Insert before cursor |
| `I` | Insert at line start |
| `a` | Append after cursor |
| `A` | Append at line end |
| `o` | Open new line below |
| `O` | Open new line above |

### Replace

| Key | Action |
|-----|--------|
| `r` | Replace single character |
| `R` | Enter replace mode |
| `cw` | Change word |
| `cc` | Change entire line |
| `C` | Change to end of line |

### Other Edits

| Key | Action |
|-----|--------|
| `J` | Join current line with next |
| `>>` | Indent line right |
| `<<` | Indent line left |
| `~` | Toggle case |
| `u` | Undo |
| `Ctrl+r` | Redo |
| `.` | Repeat last command |

---

## Deleting

### Delete Commands

| Key | Action |
|-----|--------|
| `x` | Delete character |
| `X` | Delete character before cursor |
| `dw` | Delete word |
| `dd` | Delete line |
| `D` | Delete to end of line |
| `d$` | Delete to end of line |
| `d0` | Delete to start of line |
| `dG` | Delete to end of file |
| `dgg` | Delete to start of file |

### Delete with Count

| Key | Action |
|-----|--------|
| `3dd` | Delete 3 lines |
| `5dw` | Delete 5 words |

---

## Copy & Paste

### Yank (Copy)

| Key | Action |
|-----|--------|
| `yy` | Copy current line |
| `yw` | Copy word |
| `y$` | Copy to end of line |
| `yG` | Copy to end of file |

### Paste

| Key | Action |
|-----|--------|
| `p` | Paste after cursor |
| `P` | Paste before cursor |

### Using Registers

| Key | Action |
|-----|--------|
| `"ayy` | Copy to register 'a' |
| `"ap` | Paste from register 'a' |
| `"+y` | Copy to system clipboard |
| `"+p` | Paste from system clipboard |

---

## Search & Replace

### Search

| Command | Action |
|---------|--------|
| `/pattern` | Search forward |
| `?pattern` | Search backward |
| `n` | Next match |
| `N` | Previous match |
| `:noh` | Clear highlighting |

### Replace

| Command | Action |
|---------|--------|
| `:s/old/new/` | Replace first on line |
| `:s/old/new/g` | Replace all on line |
| `:%s/old/new/g` | Replace all in file |
| `:%s/old/new/gc` | Replace with confirmation |
| `:5,10s/old/new/g` | Replace in lines 5-10 |

---

## Saving

### Save Commands

| Command | Action |
|---------|--------|
| `:w` | Save file |
| `:w filename` | Save as filename |
| `:w!` | Force save |
| `:wq` | Save and quit |
| `:x` | Save (if changed) and quit |
| `ZZ` | Save and quit |

---

## Visual Mode

### Visual Selection

| Key | Action |
|-----|--------|
| `v` | Character-wise selection |
| `V` | Line-wise selection |
| `Ctrl+v` | Block selection |
| `gv` | Reselect last selection |

### Visual Mode Operations

| Key | Action |
|-----|--------|
| `d` | Delete selection |
| `y` | Copy selection |
| `c` | Change selection |
| `>` | Indent right |
| `<` | Indent left |

---

## Multiple Files

### Buffers

| Command | Action |
|---------|--------|
| `:e filename` | Open file |
| `:bn` | Next buffer |
| `:bp` | Previous buffer |
| `:bd` | Close buffer |
| `:ls` | List buffers |

### Windows

| Command | Action |
|---------|--------|
| `:split` | Horizontal split |
| `:vsplit` | Vertical split |
| `Ctrl+w w` | Switch windows |
| `Ctrl+w q` | Close window |
| `Ctrl+w h/j/k/l` | Navigate windows |

---

## Essential Cheat Sheet

### Most Used Commands

| Task | Command |
|------|---------|
| **Enter insert mode** | `i` |
| **Exit to normal mode** | `Esc` |
| **Save** | `:w` |
| **Save and quit** | `:wq` or `ZZ` |
| **Quit without saving** | `:q!` or `ZQ` |
| **Undo** | `u` |
| **Redo** | `Ctrl+r` |
| **Delete line** | `dd` |
| **Copy line** | `yy` |
| **Paste** | `p` |
| **Find** | `/text` then `n` |
| **Replace all** | `:%s/old/new/g` |
| **Go to line 50** | `:50` or `50G` |
| **Repeat last action** | `.` |

---

## Command Mode Operations

### File Commands

| Command | Description |
|---------|-------------|
| `:e filename` | Edit/open file |
| `:w` | Write (save) file |
| `:w filename` | Save as filename |
| `:w!` | Force write |
| `:q` | Quit |
| `:q!` | Quit without saving |
| `:wq` | Write and quit |
| `:x` | Write if changed and quit |
| `:wa` | Write all buffers |
| `:qa` | Quit all |
| `:qa!` | Quit all without saving |

### Line Commands

| Command | Description |
|---------|-------------|
| `:5` | Go to line 5 |
| `:10,20d` | Delete lines 10-20 |
| `:5,10s/old/new/g` | Replace in lines 5-10 |
| `:1,5m10` | Move lines 1-5 after line 10 |
| `:1,5co10` | Copy lines 1-5 after line 10 |
| `:10r filename` | Read file after line 10 |

### Display Commands

| Command | Description |
|---------|-------------|
| `:set number` | Show line numbers |
| `:set nonumber` | Hide line numbers |
| `:set relativenumber` | Show relative numbers |
| `:set hlsearch` | Highlight search results |
| `:set nohlsearch` | No search highlight |
| `:noh` | Clear current highlighting |
| `:syntax on` | Enable syntax highlighting |
| `:syntax off` | Disable syntax highlighting |

### Buffer Commands

| Command | Description |
|---------|-------------|
| `:ls` | List all buffers |
| `:bn` | Next buffer |
| `:bp` | Previous buffer |
| `:b5` | Go to buffer 5 |
| `:bd` | Delete current buffer |
| `:bufdo command` | Execute command in all buffers |

### Window Commands

| Command | Description |
|---------|-------------|
| `:split` or `:sp` | Horizontal split |
| `:vsplit` or `:vsp` | Vertical split |
| `:new` | New horizontal split |
| `:vnew` | New vertical split |
| `:close` | Close current window |
| `:only` | Close all other windows |
| `:resize 20` | Resize window to 20 lines |
| `:vertical resize 50` | Resize window to 50 columns |

### Tab Commands

| Command | Description |
|---------|-------------|
| `:tabnew` | New tab |
| `:tabe filename` | Open file in new tab |
| `:tabn` | Next tab |
| `:tabp` | Previous tab |
| `:tabclose` | Close tab |
| `:tabonly` | Close all other tabs |
| `:tabs` | List all tabs |

### Miscellaneous Commands

| Command | Description |
|---------|-------------|
| `:!command` | Run shell command |
| `:r !command` | Read command output into file |
| `:sh` | Open shell (exit to return) |
| `:help` | Open help |
| `:help keyword` | Help on specific topic |
| `:version` | Show Vim version |
| `:echo $VIMRUNTIME` | Show Vim path |

### Settings Commands

| Command | Description |
|---------|-------------|
| `:set` | Show all changed options |
| `:set all` | Show all options |
| `:set option?` | Check option value |
| `:set option` | Turn option on |
| `:set nooption` | Turn option off |
| `:set option=value` | Set option to value |
| `:set tabstop=4` | Set tab width to 4 |
| `:set expandtab` | Use spaces instead of tabs |

---

## Advanced Commands

### Marks

| Command | Description |
|---------|-------------|
| `ma` | Set mark 'a' at cursor |
| `'a` | Jump to line of mark 'a' |
| `` `a `` | Jump to exact position of mark 'a' |
| `''` | Jump to previous position |
| `:marks` | List all marks |
| `:delmarks a` | Delete mark 'a' |
| `:delmarks!` | Delete all marks |

### Macros

| Command | Description |
|---------|-------------|
| `qa` | Start recording macro to register 'a' |
| `q` | Stop recording |
| `@a` | Play macro 'a' |
| `@@` | Repeat last macro |
| `5@a` | Play macro 'a' 5 times |

### Registers

| Command | Description |
|---------|-------------|
| `:reg` | Show all registers |
| `"ayy` | Yank line to register 'a' |
| `"ap` | Paste from register 'a' |
| `"_dd` | Delete to black hole register (no save) |
| `"+y` | Yank to system clipboard |
| `"+p` | Paste from system clipboard |

### Folding

| Command | Description |
|---------|-------------|
| `zf{motion}` | Create fold |
| `zo` | Open fold |
| `zc` | Close fold |
| `za` | Toggle fold |
| `zR` | Open all folds |
| `zM` | Close all folds |
| `zd` | Delete fold |

### Text Objects

| Command | Description |
|---------|-------------|
| `diw` | Delete inner word |
| `daw` | Delete a word (with space) |
| `dis` | Delete inner sentence |
| `das` | Delete a sentence |
| `dip` | Delete inner paragraph |
| `dap` | Delete a paragraph |
| `di"` | Delete inside quotes |
| `da"` | Delete around quotes (including quotes) |
| `di(` | Delete inside parentheses |
| `da(` | Delete around parentheses |
| `di{` | Delete inside braces |
| `ci"` | Change inside quotes |
| `yi(` | Yank inside parentheses |

---

## Quick Tips

| Tip | Description |
|-----|-------------|
| **Always start in Normal mode** | Press `Esc` if unsure |
| **Use `.` to repeat** | Most powerful command |
| **Combine commands** | `3dd` = delete 3 lines |
| **Use counts** | `5w` = move 5 words forward |
| **Practice h,j,k,l** | Faster than arrow keys |
| **Learn one at a time** | Master basics first |
| **Use :help** | Built-in documentation is excellent |
| **Text objects** | `ciw` = change inner word |

---

## Practical Examples

### Example Workflows

| Task | Command Sequence |
|------|------------------|
| **Delete word and type new** | `ciw` then type |
| **Change inside quotes** | `ci"` then type |
| **Delete 5 lines** | `5dd` |
| **Copy 3 lines** | `3yy` |
| **Replace all "foo" with "bar"** | `:%s/foo/bar/g` |
| **Delete from cursor to end** | `d# ⌨️ Vi/Vim Shortcuts - Quick Reference

> Essential keyboard shortcuts for Vi/Vim text editor

---

## 📑 Table of Contents

| Section | Description |
|---------|-------------|
| [Modes](#modes) | Understanding Vi modes |
| [Starting & Quitting](#starting--quitting) | Open and close files |
| [Navigation](#navigation) | Move around |
| [Editing](#editing) | Insert and modify text |
| [Deleting](#deleting) | Remove text |
| [Copy & Paste](#copy--paste) | Clipboard operations |
| [Search & Replace](#search--replace) | Find and replace |
| [Saving](#saving) | Save files |

---

## Modes

### Vi Modes

| Mode | How to Enter | Purpose |
|------|--------------|---------|
| **Normal** | `Esc` | Navigate and run commands (default) |
| **Insert** | `i`, `a`, `o` | Type text |
| **Visual** | `v`, `V` | Select text |
| **Command** | `:` | Execute commands |

---

## Starting & Quitting

### Opening Files

| Command | Description |
|---------|-------------|
| `vi filename` | Open file |
| `vi +10 filename` | Open at line 10 |
| `view filename` | Open read-only |

### Exiting

| Command | Description |
|---------|-------------|
| `:q` | Quit (if no changes) |
| `:q!` | Quit without saving |
| `:wq` | Save and quit |
| `:x` | Save (if changed) and quit |
| `ZZ` | Save and quit (shortcut) |
| `ZQ` | Quit without saving (shortcut) |

---

## Navigation

### Basic Movement

| Key | Action |
|-----|--------|
| `h` | Left |
| `j` | Down |
| `k` | Up |
| `l` | Right |

### Word Movement

| Key | Action |
|-----|--------|
| `w` | Next word start |
| `b` | Previous word start |
| `e` | Next word end |

### Line Movement

| Key | Action |
|-----|--------|
| `0` | Start of line |
| `^` | First non-blank character |
| `$` | End of line |

### Page Movement

| Key | Action |
|-----|--------|
| `gg` | First line of file |
| `G` | Last line of file |
| `10G` | Go to line 10 |
| `Ctrl+f` | Page down |
| `Ctrl+b` | Page up |
| `Ctrl+d` | Half page down |
| `Ctrl+u` | Half page up |

### Search Navigation

| Key | Action |
|-----|--------|
| `/text` | Search forward for "text" |
| `?text` | Search backward for "text" |
| `n` | Next search result |
| `N` | Previous search result |
| `*` | Search word under cursor |

---

## Editing

### Insert Mode

| Key | Action |
|-----|--------|
| `i` | Insert before cursor |
| `I` | Insert at line start |
| `a` | Append after cursor |
| `A` | Append at line end |
| `o` | Open new line below |
| `O` | Open new line above |

### Replace

| Key | Action |
|-----|--------|
| `r` | Replace single character |
| `R` | Enter replace mode |
| `cw` | Change word |
| `cc` | Change entire line |
| `C` | Change to end of line |

### Other Edits

| Key | Action |
|-----|--------|
| `J` | Join current line with next |
| `>>` | Indent line right |
| `<<` | Indent line left |
| `~` | Toggle case |
| `u` | Undo |
| `Ctrl+r` | Redo |
| `.` | Repeat last command |

---

## Deleting

### Delete Commands

| Key | Action |
|-----|--------|
| `x` | Delete character |
| `X` | Delete character before cursor |
| `dw` | Delete word |
| `dd` | Delete line |
| `D` | Delete to end of line |
| `d$` | Delete to end of line |
| `d0` | Delete to start of line |
| `dG` | Delete to end of file |
| `dgg` | Delete to start of file |

### Delete with Count

| Key | Action |
|-----|--------|
| `3dd` | Delete 3 lines |
| `5dw` | Delete 5 words |

---

## Copy & Paste

### Yank (Copy)

| Key | Action |
|-----|--------|
| `yy` | Copy current line |
| `yw` | Copy word |
| `y$` | Copy to end of line |
| `yG` | Copy to end of file |

### Paste

| Key | Action |
|-----|--------|
| `p` | Paste after cursor |
| `P` | Paste before cursor |

### Using Registers

| Key | Action |
|-----|--------|
| `"ayy` | Copy to register 'a' |
| `"ap` | Paste from register 'a' |
| `"+y` | Copy to system clipboard |
| `"+p` | Paste from system clipboard |

---

## Search & Replace

### Search

| Command | Action |
|---------|--------|
| `/pattern` | Search forward |
| `?pattern` | Search backward |
| `n` | Next match |
| `N` | Previous match |
| `:noh` | Clear highlighting |

### Replace

| Command | Action |
|---------|--------|
| `:s/old/new/` | Replace first on line |
| `:s/old/new/g` | Replace all on line |
| `:%s/old/new/g` | Replace all in file |
| `:%s/old/new/gc` | Replace with confirmation |
| `:5,10s/old/new/g` | Replace in lines 5-10 |

---

## Saving

### Save Commands

| Command | Action |
|---------|--------|
| `:w` | Save file |
| `:w filename` | Save as filename |
| `:w!` | Force save |
| `:wq` | Save and quit |
| `:x` | Save (if changed) and quit |
| `ZZ` | Save and quit |

---

## Visual Mode

### Visual Selection

| Key | Action |
|-----|--------|
| `v` | Character-wise selection |
| `V` | Line-wise selection |
| `Ctrl+v` | Block selection |
| `gv` | Reselect last selection |

### Visual Mode Operations

| Key | Action |
|-----|--------|
| `d` | Delete selection |
| `y` | Copy selection |
| `c` | Change selection |
| `>` | Indent right |
| `<` | Indent left |

---

## Multiple Files

### Buffers

| Command | Action |
|---------|--------|
| `:e filename` | Open file |
| `:bn` | Next buffer |
| `:bp` | Previous buffer |
| `:bd` | Close buffer |
| `:ls` | List buffers |

### Windows

| Command | Action |
|---------|--------|
| `:split` | Horizontal split |
| `:vsplit` | Vertical split |
| `Ctrl+w w` | Switch windows |
| `Ctrl+w q` | Close window |
| `Ctrl+w h/j/k/l` | Navigate windows |

 or `D` |
| **Go to line 100** | `:100` or `100G` |
| **Save as new file** | `:w newfile.txt` |
| **Edit another file** | `:e otherfile.txt` |
| **Split and edit** | `:vsp file.txt` |

### Common Tasks

| Task | Best Command |
|------|--------------|
| **Format JSON** | `:%!python -m json.tool` |
| **Sort lines** | `:%!sort` |
| **Remove duplicate lines** | `:sort u` |
| **Delete empty lines** | `:g/^$/d` |
| **Delete lines with pattern** | `:g/pattern/d` |
| **Convert tabs to spaces** | `:retab` |
| **Show whitespace** | `:set list` |
| **Auto-indent file** | `gg=G` |

---

**Remember:** Press `Esc` to return to Normal mode anytime!

Type `:help` in Vim to access the built-in comprehensive documentation.
