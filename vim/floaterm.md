## Vim-floaterm

![](https://www.youtube.com/watch?v=QzlwC-AUY-U)

* Plugin: https://github.com/voldikss/vim-floaterm
* Install: `Plug 'voldikss/vim-floaterm'`
* For neovim, also install `pip3 install neovim-remote` to allow floaterm to open windows inside neovim
* Keybindings:
  * new: `let g:floaterm_keymap_new = '<Leader>ft'`
  * toggle: `let g:floaterm_keymap_toggle = '<Leader>t'`
* Most important, enter normal mode inside floating terminal: `<C-\><C-n>`:
  * Allows you to both navigate inside the terminal like in normal mode.
  * And run commands like `:FloatermNext` to scroll through floaterm terminals
* Can also open random repls like python or lua: `:FloatermNew python`
  * Can send selected text to the repl (or a terminal really), using `:FloatermSend`
* Primarily use it for C++ build/test runs. 
