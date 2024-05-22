# Resources
- `nvim` then `:Tutor`
- https://www.openvim.com/
- https://learnxinyminutes.com/docs/vim/ (DONT DO SHIT AT BOTTOM IN `~/.VIMRC`)
#  Tutorial Specific 
- Links - put the cursor over the link and type `Enter`
- control + character is specified by `<C-[char]>`
- Super (Meta) + character is specified by `<S-[char]>` or `<M-[char]>`
# Help
- help for nvim: `:h <what you need help with>`

# Navigation Commands
- Exiting (just closing the window) - `:q`
- Exiting (no save): `:q!`
- Movement: `h, j, k, l`
- go-back (to jumps, previous files, etc.): `<cntrl> o`

### Jumping Around
- paragraphs: 
	- up  `(`
	- down  `)`

# Commands
- delete word: go to a word and type `dw`
- deleting line: go to the end of the correct line and type `d$`
	- this deletes everything after your cursor 
### Ex commands `:`
all commands that begin with `:` are called ex commands

# Editing
- Deletion:  go over the char you want deleted and press `x`
- Appending Text: Go to the line you want to append to and press `A`

# Files
- write-and-quit: `:wq`
- creating a file : `nvim <file_name>`

# Motions 
many commands that change text are made from an **operator** and a **motion**.

*Example:*
the format for a delete command with the `d` delete operator is as follows:
			`d <motion>`
- d - the delete operator 
- motion - what the operator will operate on 

### Motion Counts 
motions can be repeated by specifying a constant value to apply the motion by. For example, `3w` is equivalent to pressing `w` 3 times.  
- counts may be applied to any motion 

### Common Motions
- `w` - until the start of the next word **EXCLUDING** the first character (this includes symbols in general) (*to only use whitespace as delimeters use `W`*) 
- `b` - backwards to the start of the last word (*to only use whitespace as delimeters use `B`*) 
- `e` - jump to the end of the current word **INCLUDING** the last character (*to only use whitespace as delimeters use `E`*) 
- `$` - jump to the last character of the current line 
- `0` - to move to the first position of the current line
- `^` - moves to the first non white-space character of a line 

### Undo `u`
undoes the last command 

### Redo `<C-r>`
redoes the last command 

### Insertion  `i`
enters insert mode 
- counts can be applied to it - `3itest` outputs `testtesttest`

### Go-to `gg`, `G`
applying counts to these motions will take you to specific line number specified by the count 
- `gg` takes you to the beginning of the file 
- `G` takes you to the end of the file (applying a count to this does the exact same thing as `gg`)

### Weird Shit ;) 
- `<C-d>` - cntrl + d -> moves half a page down on the current screen
- `<C-u>` - cntrl + d -> moves half a page up 

### Next Character Occurrence `f`, `F` ,`t`, `T`, `;`
this command only works within the current line that you are in (this only works for characters). If that character does not exist on the current line, nothing will happen. 
- `f` - moves to next occurrence 
- `F` - moves to the previous occurrence 
- `t` - moves to the character before the next occurrence of that character 
- `T` - moves to the character after the previous occurrence of that character
- `;` - repeats the previously used operator from this list (note that the count will not be applied again)
### Enclosing Symbols `%`
`%` will jump to the matching enclosing symbol to the one you cursor is on. 

### Searching `/`,`?`,`*`,`#`
- `/` - allows you to specify text to search forward from your current position 
- `?` - the same as `/` but reverse
- `*` - searches for the next occurrence of the word your cursor is currently over 
- `#` - the same as `*` but in reverse
# Operators
_Operators_ let you operate in a range of text (defined by motion). 
- `y` - yank
- `yy` - yank whole line 
- `Y` - equivalent to doing `y$` (from cursor position to end of line)

*in the same way, the `d` and `c` motions can be used*

### Change `c`
equivalent to doing `d <motion> i`. After deleting to the specified motion, you are immediately placed into insert mode.

*note: `cw` and `ce` have the exact same functionality as `ce`*


# Visual Mode 
visual mode consists of 3 separate types of modes. All of them are used to highlight or select text.

*Note: Operators function the same way across all visual modes but in the context of that visual mode. Operators just work on whats selected by the mode.* 

### Visual Character `v`
normal highlighting behavior. Just goes from where your cursor is currently at to some end point.

### Visual Line `V` (Capital v)
this mode will only select full lines of text no matter the motion given. 

### Visual Block `<C-v>` (cntrl v)
this mode will highlight a square block from where your cursor is to the end. (you define the size of the block that will be highlighted)

# Recording 
1. press `q` to start recording mode
2. select a register key to save the recording to (as a macro) (do q by default) so press `q`
3. record your motion 
4. press `q` to stop your recording 
5. to play back, input `@` and the register key that your recording was saved to 

