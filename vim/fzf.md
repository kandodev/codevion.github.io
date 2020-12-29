# fzf 
* Youtube video: https://www.youtube.com/watch?v=DpURGnb4Fyk
[](https://www.youtube.com/watch?v=DpURGnb4Fyk)

* Plugin: https://github.com/junegunn/fzf.vim
```
Plug 'junegunn/fzf', { 'do': { -> fzf#install() } }
Plug 'junegunn/fzf.vim'
```
* Ctrl-p to search: `nnoremap <C-p> :Files<Cr>`
* Search in full screen window: `:Files!`
* Can search for other things, e.g: `:Buffers`
* Within a search:
  * Arrow keys to navigate up and down, or `<C-n>` and `<C-p>`
  * `Enter` to open in current window
  * `<C-t>` to open in new tab
  * `<C-v>` to open in vertical split
  * `<C-x>` to open in horizontal split
* fzf window appearance:
  * Bottom: `let g:fzf_layout = { 'down': '40%' }`
  * Popup: `let g:fzf_layout = { 'window': { 'width': 0.9, 'height': 0.6 } }`
* Project files:
  * Taken from https://github.com/junegunn/fzf.vim/issues/47
  * Can use https://github.com/airblade/vim-rooter
* Codevion.github.io
