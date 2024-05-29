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