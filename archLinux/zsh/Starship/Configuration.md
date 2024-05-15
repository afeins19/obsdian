
- [[#Escaping Strings|Escaping Strings]]
- [[#Declaring Strings|Declaring Strings]]
	- [[#Declaring Strings#Examples of String Declarations|Examples of String Declarations]]
- [[#Format Strings|Format Strings]]
		- [[#Examples of String Declarations#Examples of Format Strings|Examples of Format Strings]]
- [[#Text Groups|Text Groups]]
		- [[#Examples of String Declarations#Examples of Text Groups|Examples of Text Groups]]
		- [[#Examples of String Declarations#Examples of Style Strings|Examples of Style Strings]]
- [[#Conditional Format Strings|Conditional Format Strings]]
		- [[#Examples of String Declarations#Examples of Conditional Format Strings|Examples of Conditional Format Strings]]
- [[#Negative Matching|Negative Matching]]
- [[#Right Prompt|Right Prompt]]
- [[#Example of Right Format|Example of Right Format]]
- [[#Continuation Prompt|Continuation Prompt]]
		- [[#Examples of String Declarations#Example of Continuation Prompt|Example of Continuation Prompt]]
- [[#Colors|Colors]]
		- [[#Examples of String Declarations#Cautions|Cautions]]

# Introductory Note 
First make sure the configuration file exists (`~/.config/starship.toml`). All of the configuration of starship is done in this TOML file. 

# Logging 
by default starship logs are put into `~/.cache/starship/session_${STARSHIP_SESSION_KEY}.log`. You can change this by doing the following export: `export STARSHIP_CACHE=~/.starship/cache`

# Terminology 

**Module**: A component in the prompt giving information based on contextual information from your OS. For example, the "nodejs" module shows the version of Node.js that is currently installed on your computer, if your current directory is a Node.js project.

**Variable**: Smaller sub-components that contain information provided by the module. For example, the "version" variable in the "nodejs" module contains the current version of Node.js

By convention, most modules have a prefix of default terminal color (e.g. `via` in "nodejs") and an empty space as a suffix.
# Strings 

### Escaping Strings 
the following symbols must be used to escape special characters. These must be used in a format string: `$ [ ] ( )`. 
### Declaring Strings 
In TOML the following characters are used to declare strings

| **Symbol** | **Type**                  | **Notes**                                               |
| ---------- | ------------------------- | ------------------------------------------------------- |
| `'`        | literal string            | less escaping                                           |
| `"`        | string                    | more escaping                                           |
| `'''`      | multi-line literal string | less escaping                                           |
| `"""`      | multi-line string         | more escaping, newlines in declarations can be ignored  |
#### Examples of String Declarations
```toml 
# literal string
format = '☺\☻ '

# regular string
format = "☺\\☻ "

# escaping Starship symbols
format = '\[\$\] '
```

When using line breaks, multi-line declarations can be used. For example, if you want to print a `$` symbol on a new line, the following values for `format` are equivalent:

```toml
# with literal string
format = '''

\$'''

# with multiline basic string
format = """

\\$"""

# with basic string
format = "\n\\$"
```

with basic multiline strings, newlines can bbe used for formatting without the escapes being present. If the escape symbols are present, they'll be ignored. 

```toml
format = """
line1\
line1\
line1
line2\
line2\
line2
"""
```
### Format Strings 
format strings are the format that a module prints all its variables with. Most variables have an entry called `format` that configures the display format of the module. We can put text, variables, and [[#Text Groups]] into a format string 

##### Examples of Format Strings 
- `'$version'` is a format string with a variable named `version`.
- `'$git_branch$git_commit'` is a format string with two variables named `git_branch` and `git_commit`.
- `'$git_branch $git_commit'` has the two variables separated with a space.
### Text Groups
a text group consists of two different parts 
1.  **Format String** - enclosed in `[]`. You can add text, variables, or even nest text groups into it. 
2. **Style String** - enclosed in `()`. This is used to apply styling to the Format String. 

Full Syntax: [advanced config guide](https://starship.rs/advanced-config/)
##### Examples of Text Groups 
- `'[on](red bold)'` will print a string `on` with bold text colored red.
- `'[⌘ $version](bold green)'` will print a symbol `⌘` followed by the content of variable `version`, with bold text colored green.
- `'[a [b](red) c](green)'` will print `a b c` with `b` red, and `a` and `c` green.

##### Examples of Style Strings 
- `'fg:green bg:blue'` sets green text on a blue background
- `'bg:blue fg:bright-green'` sets bright green text on a blue background
- `'bold fg:27'` sets bold text with [ANSI color](https://i.stack.imgur.com/KTSQa.png) 27
- `'underline bg:#bf5700'` sets underlined text on a burnt orange background
- `'bold italic fg:purple'` sets bold italic purple text
- `''` explicitly disables all styling

*Note that what styling looks like will be controlled by your terminal emulator.*

### Conditional Format Strings 
A conditional format string wrapped in `(` and `)` will not render if all variables inside are empty.

##### Examples of Conditional Format Strings
- `'(@$region)'` will show nothing if the variable `region` is `None` or empty string, otherwise `@` followed by the value of region.
- `'(some text)'` will always show nothing since there are no variables wrapped in the braces.
- When `$combined` is a shortcut for `\[$a$b\]`, `'($combined)'` will show nothing only if `$a` and `$b` are both `None`. This works the same as `'(\[$a$b\] )'`.

### Negative Matching 
Many modules have `detect_extensions`, `detect_files`, and `detect_folders` variables. These take lists of strings to match or not match. "Negative" options, those which should not be matched, are indicated with a leading '!' character. The presence of _any_ negative indicator in the directory will result in the module not being matched.

For example, `foo.bar.tar.gz` will be matched against `bar.tar.gz` and `gz` in the `detect_extensions` variable. Files whose name begins with a dot are not considered to have extensions at all.

# Prompt 
the full list of prompt-wide configuration options

| **Option**     | **Default**         | **Description**             |
| -------------- | ------------------- | --------------------------- |
| `format`       | [[#Format Strings]] | configure the prompt format |
| `right_format` | `''`                |                             |
|                |                     |                             |
### Right Prompt 
if your shell supports a right prompt on the same line as the user input line. This content can be set using `right_format`. All options supported by the `format` option are supported in `right_format`. The `$all` variable will only contain modules not explicitly used in either `format` or `right_format`.

*Note: The [Ble.sh](https://github.com/akinomyoga/ble.sh) framework v0.4 or higher should be installed in order to use right prompt in bash.*

### Example of Right Format 
```toml
# ~/.config/starship.toml

# A minimal left prompt
format = """$character"""

# move the rest of the prompt to the right
right_format = """$all"""
```

produces this output 
```sh
▶                                   starship on  rprompt 
```
- `format` = """▶"""
- `right_format`="""starship on  rprompt """

### Continuation Prompt 
this prompt is used when the user entered an incomplete statement such as an open parenthesis or quote. 

*Note: `continuation_prompt` should be set to a literal string without any variables.*

##### Example of Continuation Prompt 
```
# ~/.config/starship.toml

# A continuation prompt that displays two filled in arrows
continuation_prompt = '▶▶ '
```

# Style-Strings 
Style strings are a list of words, separated by whitespace. The words are not case sensitive (i.e. `bold` and `BoLd` are considered the same string). Each word can be one of the following: 
- `bold`
- `italic`
- `underline`
- `dimmed`
- `inverted`
- `blink`
- `hidden`
- `strikethrough`
- `bg:<color>`
- `fg:<color>`
- `<color>`
- `none`

where `<color>` is a color specifier (discussed below). `fg:<color>` and `<color>` currently do the same thing, though this may change in the future. `inverted` swaps the background and foreground colors. The order of words in the string does not matter.

`none` overrides all other tokes in the a string if it is not part of a `bg:` specifier. e.g. `fg:red none fg:blue` will still create a string with no styling. `bg:none` sets the background to the default color so `fg:red bg:none` is equivalent to `red` or `fg:red` and `bg:green fg:red bg:none` is also equivalent to `fg:red` or `red`. It may become an error to use `none` in conjunction with other tokens in the future.

### Colors 
you can specify colors in the folllowing ways: 
- **standard terminal colors** - `black`, `red`, `green`, `blue`, `yellow`, `purple`, `cyan`, `white`. You can optionally prefix these with `bright-` to get the bright version (e.g. `bright-white`).
- **Hexadecimal** - using `#` followed by a hex-code 
- **ANSI 8-bit RGB** - a value between 0-255

*note: If multiple colors are specified for foreground/background, the last one in the string will take priority.*

##### Cautions
- Many terminals disable support for `blink` by default
- `hidden` is [not supported on iTerm](https://gitlab.com/gnachman/iterm2/-/issues/4564).
- `strikethrough` is not supported by the default macOS Terminal.app