# Lazy
nvim's plugin manager.
- to open lazy type `:Lazy` (the 'l' is capitalized)
- to close out of lazy, type `q`

# Command Bar
- `:e <filname>` open a file to edit. if no file is specified, it will just reload the current file.  
# Autocompletions in NVIM
autocompletion works just like it does in the terminal with tab to cycle through 

# Getting Started with Neovim Video 

# Kickstart
a template for creating your custom configuration of Neovim

# Helpful Commands
- `:tutor` - runs the neovim tutor 
- `:help` - runs the neovim help application 
- `<space> sh` - opens the search menu in the help documentation directory

# Searching
initiate a search with the leader key: `<space>`. you can then give the following sub-commands for a specific kind of search.
- `sh` - search help

# Key mappings (`lspconfig.lua`)
these are key mappings that we can define for the language server protocol (lsp).
- `gd` - goto definition (go to where a function or variable is defined)
- `gr` goto references (find all references in this file of what your cursor is currently over)
- `gI` 0- goto implementation (when a variable is declared but not assigned a value `int i;`)
- `gD` - goto **Decleration**, note that this is not the definition 
- `<space>D` - type Definition (used when you want to find the *type* definition of a variable... see the definition of the type for that variable)
- `<space>ds` - fuzzy search over all symbols in the current **document** (symbols are things like variables functions, types, other keyword delimited strings)
- `<space>ws` - fuzzy search over the entire **workspace** (same as `<space>ds` but over the entire project)
- `<space>rn` - rename the variable under your cursor 
- `<space>ca` - execute a code action? (get a suggestion from the LSP for dealing with some error i think)
- `K` - (shift+k) - opens a popup that displays documentation about the word under your cursor 

# Auto-completion Commands
definitions are found in `cmp.lua`
```Lua

-- For an understanding of why these mappings were
-- chosen, you will need to read `:help ins-completion`
-- No, but seriously. Please read `:help ins-completion`, it is really good!
```

### Source 
sources can hold plugins and completion sources that generate suggestions and group them together. This means that all will be used in generating auto-completion statements. 

### Cycling through suggestions
when a dialog box appears displaying possible options to autocomplete, use the following keys to cycle through them - `<C-<char>> = cntrl+<char>`
- `<C-n>` - toggle next item 
- `<C-p>` - toggle previous item 
- `<C-y>` - confirm the selection 

### Comments
there are special kinds of comment types that get unique syntax highlighting and recieve their expected functionalities. This is from `folke/todo-comments.nvim`.
- `--note <note_text>` - creates a NOTE type comment
- `--todo <todo_text>` - creates a TODO type comment 
- `--fixme <fix_me_text>` - creates a FIXME type comment 

