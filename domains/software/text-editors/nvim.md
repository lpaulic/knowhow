# [Neo Vim](https://neovim.io/)

## Configuration

Personal nvim configuration can be found [here](https://github.com/lpaulic/dotfiles/tree/master/config/nvim).

## General
The screen is consisted of a `buffer`. A `buffer` is a representation of a file system file/directory in memory.
A `window` is a view of a buffer, in other words a window contains a `buffer`.
There can be multiple `window` containing the same `buffer`.

## Vim modes
- Normal mode -> Esc, Ctrl+{
- Visual mode -> v
  - Includes just the selection in commands
- visual line mode -> Shift+v
  - Includes new line with selection in commands
- Insert mode -> i, a, I, A
- Command mode -> :

Basic structure of input to vim: `Command Count Motion`

## Vim commands
File commands:
- Esc, Ctr+{ -> goes to Normal mode
- i -> moves the cursor to the left of the character goes to insert mode
- I -> moves the cursor to the beginning of the line and goes to insert mode
- a -> moves the cursor to the right of the character goes to insert mode
- A ->  moves the cursor to the end of the line and goes to insert mode
- o -> adds a new line below cursor position, moves the cursor to the beginning of the new line and goes to insert mode
- Shift+o -> adds a new line above cursor position, moves the cursor to the beginning of the new line and goes to insert mode
- : -> goes into command mode
- v -> goes into visual mode
- Shift+v -> goes into visual-line mode
- d -> delete
- y -> yank
- p -> paste
- u -> undo last command
- Ctrl+r -> redo previous command

Window commands:
- Ctrl+w s -> splits current window in two

Commands can be combined with `Count` and `Motion`, i.e.:
- d4j -> delete 4 lines down
- d5l -> delete for characters right

### Useful information
Yanking and deleting go to the same buffer. Meaning that if we paste something
over the content that has been pasted over will be in the buffer.

We do not need to be in visual mode to use yank and delete commands.

## Vim motions
Motions in normal and visual/visual-line modes:
- j -> cursor goes upwards
- k -> cursor goes downwards
- l -> cursor goes right
- h -> cursor goes left
- w -> cursor goes right by a word
- b -> cursor goes left by a word
- _ -> cursor goes to the beginning of the line
- $ -> cursor goes to the end of the line
- 0 -> cursor goes to the first character on the line
- f<character> -> cursor goes to the right on the <character>
- F<character> -> cursor goes to the left on the <character>
- t<character> -> cursor goes to the right up to the <character>
- T<character> -> cursor goes to the right up to the <character>
- , -> goes to the next character, right for the f and t searches, left for the F and T searches
- ; -> goes to the previous character, left for the f and t searches, right for the F and T searches
- gg -> goes to the beginning of the file
- G -> goes to the end of the file

## Advanced motions
- vi<enclosing-character-open-or-close> -> select everything between the brackets, regardless of the cursor position, not including the brackets
- va<enclosing-character-open-or-close> -> select everything between the brackets, regardless of the cursor position, including the brackets
- yi<enclosing-character-open-or-close> -> yanks everything between the brackets, regardless of the cursor position, not including the brackets
- yi<enclosing-character-open-or-close> -> yanks everything between the brackets, regardless of the cursor position, including the brackets
- viw, vaw -> selects the word where the cursor under the cursor
- yiw, yaw -> yank the word where the cursor under the cursor
- viW -> select all character under the cursor until whitespace from both end
- yiW -> yank all character under the cursor until whitespace from both end
- Vy -> select whole line under the cursor and yank it
- ci<enclosing-character-open-or-close> -> deletes everything between the characters, regardless of the cursor position, not including the brackets, goes to insert mode
- ca<enclosing-character-open-or-close> -> deletes everything between the characters, regardless of the cursor position, including the brackets, goes to insert mode
- o -> when in visual mode and multiple lines are selected jumps to start/end of the selection
- yap -> yank continuous lines of text, including the new line
- dap -> delete continuous lines of text, including the new line
- yip -> yank continuous lines of text, not including the new line
- dip -> delete continuous lines of text, including the new line
- cgn -> change the first occurrence of a selected text, use . to change the next occurrence, use n to skip

## Recording macros
Store multiple actions and movements in a buffer that can than be "replayed".
To start recording a macro, enter normal mode than press:
1. Press `q`
2. Use any alphanumeric character as the register to store the recording (for example, a)
3. Execute command sequence to accomplish the required task
4. Press `q` again to stop recording
5. Press `@a` to execute the recorded sequence of actions

The recorded sequence can be combined with the count.

## References and links
1. [Vim motions in nvim](https://neovim.io/doc/user/motion.html#motion.txt)
2. [Vim windows](https://neovim.io/doc/user/windows.html#windows-intro)
3. [0 to LSP : Neovim RC From Scratch; ThePrimeagen](https://www.youtube.com/watch?v=w7i4amO_zaE)
4. [Vim As Your Editor - Horizontal](https://www.youtube.com/watch?v=5JGVtttuDQA)
4. [Vim As Your Editor - Vertical Movements](https://www.youtube.com/watch?v=KfENDDEpCsI)
5. [Vim As You Editor - Advanced Motions P1](https://www.youtube.com/watch?v=qZO9A5F6BZs)
6. [Vim As You Editor - Advanced Motions P2](https://www.youtube.com/watch?v=uL9oOZStezw)
7. [From 0 to IDE in NEOVIM from scratch | FREE COURSE // EP 1](https://www.youtube.com/watch?v=zHTeCSVAFNY)
8. [A BEAUTIFUL neovim config with Lazy | FREE COURSE // EP 2 ](https://www.youtube.com/watch?v=4zyZ3sw_ulc)
9. [LSP in Neovim. Thanks to BILL GATES?! | FREE COURSE // EP 3](https://www.youtube.com/watch?v=S-xzYgTLVJE)
10. [hat the hell is NULL-LS | FREE COURSE // EP 4](https://www.youtube.com/watch?v=SxuwQJ0JHMU)
11. [Autocomplete and Snippets in Neovim | FREE COURSE // EP 5 ](https://www.youtube.com/watch?v=iXIwm4mCpuc)
12. [You don’t need more than one cursor in vim](https://medium.com/@schtoeffel/you-don-t-need-more-than-one-cursor-in-vim-2c44117d51db)
