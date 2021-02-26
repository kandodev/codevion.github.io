# Telescope! 
* https://github.com/nvim-telescope/telescope.nvim
* Requires neovim-nightly (0.5+): `yay -S neovim-git` on arch
* Requires ripgrep: `pacman -S ripgrep` on arch
* Installation:
```
Plug 'nvim-lua/popup.nvim'
Plug 'nvim-lua/plenary.nvim'
Plug 'nvim-telescope/telescope.nvim'
```
* Usage key mappings:
  * `<C-n>`,`<C-p>` for next/previous item
  * `<C-d>`, `<C-u>` for scrolling up/down in preview window
  * `<C-x>`, `<C-v>`, `<C-t>` for opening in split, vsplit, new tab
  * `<CR>` to confirm selection
* Some basic picker trigger key mappings:
```
" Find files using Telescope command-line sugar.
nnoremap <leader>ff <cmd>Telescope find_files<cr>
nnoremap <leader>fg <cmd>Telescope live_grep<cr>
nnoremap <leader>fb <cmd>Telescope buffers<cr>
nnoremap <leader>fh <cmd>Telescope help_tags<cr>
```
* Other pickers here: https://github.com/nvim-telescope/telescope.nvim#pickers
* Ones I think I'll find personally useful:
  * `builtin.oldfiles`
  * `builtin.tags`: for projects using ctags
  * `builtin.man_pages`
  * LSP/Treesitter ones when I start using those. (Haven't been able to get it to work with CoC yet)
