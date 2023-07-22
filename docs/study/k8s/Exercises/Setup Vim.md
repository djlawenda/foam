---
type: basic-note
foam_template:
    name: basic-note
    description: Basic note
    filepath: 'new/Setup Vim.md'
---
# Setup Vim
Note Created: 2023-02-26

## Note

### Create .vimrc
```console
vim ~/.vimrc
```
```yaml
set expandtab # expandtab: use spaces for tab
set tabstop=2 # tabstop: amount of spaces used for tab
set shiftwidth=2 # shiftwidth: amount of spaces used during indentation
```

### Set line numbers
Normal Mode enter :set number

### Set intend to 2
Normal Mode enter :set shiftwidth=2

### Set paste to keep indent
Normal Mode enter :set paste

### Search
Normal Mode press / and phrase to search
Go to next press n
Go to previous press N

### Change indent for multipl lines
Normal Mode enter :set shiftwidth=2
Go to line and press Shit+V to enter Visual Mode
Select rows with arrows up or down
Move the selected block to right press Shit+>
Move the selected block to left press Shit+,

### Navigate
Normal Mode
| shortcut | function |
|----------|----------|
|[[       |first line|
|]]       |last line|
|:number  |jump to line|
|h        |moves the cursor one character to the left|
|j        |moves the cursor down one line|
|k        |moves the cursor up one line|
|l        |moves the cursor one character to the right|
|0        |zero, moves the cursor to the beginning of the line|
|$        |moves the cursor to the end of the line|
|w        |move forward one word|
|b        |move backward one word|
|5w       |move forward five words|
|5b       |move backward five words|
|/word    |search word, string pattern|
|n        |jump to next occurance|
|N        |jump to previous occurance|
|\\<word\\>    |search exact word|
|:s/word1/word2/    |replace word1 with word2 one time|
|:s/word1/word2/g    |replace word1 with word2 everywhere|

### Activate insert mode
Insert Mode
| shortcut | function |
|----------|----------|
|o         |insert new line below|
|O         |insert new line above|
|a         |append after coursor|
|A         |append at the end of line|

### Delete
Normal Mode
| shortcut | function |
|----------|----------|
|dd        |delete the line|
|d$        |Delete from current position to end of line|
|d0        |Delete from current backward to beginning of line|
|dw        |Delete current to end of current word|
|db        |Delete current to beginning of current word|
|.,$d      |Delete From Current Line to the End of File|
|dgg       |Delete From Current Line to the Beginning of File|
|dG        |clear the file completely|

### Copy, Cut, Paste
Normal Mode
| shortcut | function |
|----------|----------|
|ggVG      |select all|
|yy        |copy the line|
|p         |paste to line after cursor|
|P         |paste to line before cursor|
|yiw       |copy current word|

> !!! In CKAD exam vim to paste Shift+Insert
> !!! In CKAD exam vim to copy Ctrl+Insert




