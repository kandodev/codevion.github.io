### (Neo)vim for C++ Part 2: CMake, GTest, File Explorer, etc

[](https://www.youtube.com/watch?v=Y_UubM5eYAM)

#### Pre-requisites:
  * [Neovim for C++ 1: CoC](coc.md)
  * [fzf](fzf.md)
  * [floaterm](floaterm.md)

#### Ref
* Source code available at: https://github.com/codevion/tutorial_dots/tree/main/cpp2 

#### Tutorial
* Some keybindings for comfort:

```
nnoremap <c-j> <c-w>j
nnoremap <c-h> <c-w>h
nnoremap <c-k> <c-w>k
nnoremap <c-l> <c-w>l

" Save on Ctrl-S
nmap <c-s> :w<CR>
imap <c-s> <Esc>:w<CR>a
```

* File explorer: 
    * fff: `sudo pacman -S fff`
    * `nmap <c-t> :FloatermNew fff<cr>`
* Build integration:
  * CMake: `sudo pacman -S cmake`
  * Basic CMake setup
  * Building CMake from the command line
  * Using [vim-cmake](https://github.com/cdelledonne/vim-cmake)
    * `Plug 'cdelledonne/vim-cmake'`
      * For neovim, also do: `Plug 'antoinemadec/FixCursorHold.nvim'`
    * `let g:cmake_link_compile_commands = 1`
    * `:CMakeGenerate` to generate cmake files.
    * `:CMakeBuild` to build them
    * Easier keybindings:
      * `nmap <leader>cg :CMakeGenerate<cr>`
      * `nmap <leader>cb :CMakeGenerate<cr>`
* Test integration:
  * Setup CMake and GoogleTest. 
  * Install vim-gtest: https://github.com/alepez/vim-gtest
    * `Plug 'alepez/vim-gtest'`
  * Need to set the binary for testing:
    * `:GTestCmd path/to/test/executable`
    * Or `let g:gtest#gtest_command = "path/to/test/executable"` in your vimrc
  * The most useful is: `:GTestRunUnderCursor`
  * Easier keybinding:
    * `nmap <leader>gt :GTestRunUnderCursor<cr>`
