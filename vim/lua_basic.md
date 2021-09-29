# Basic Lua Configuration for Neovim

* Based on video in https://www.youtube.com/watch?v=ppMX4LHIuy4
[](https://www.youtube.com/watch?v=ppMX4LHIuy4)

## Set basic configurations
```
vim.opt.expandtab = true
vim.opt.shiftwidth = 2
vim.opt.softtabstop = 2
```

## Set up keymaps
```
local keymap = vim.api.nvim_set_keymap
keymap('n', '<c-s>', ':w<CR>', {})
keymap('i', '<c-s>', '<Esc>:w<CR>a', {})
local opts = { noremap = true }
keymap('n', '<c-j>', '<c-w>j', opts)
keymap('n', '<c-h>', '<c-w>h', opts)
keymap('n', '<c-k>', '<c-w>k', opts)
keymap('n', '<c-l>', '<c-w>l', opts)
```

## Set up Package management
```
require('packer').startup(function()
  use 'wbthomason/packer.nvim'

  use 'tomasr/molokai'
end)

vim.g.colors_name = 'molokai'
```

Can add more complex configuration inside package management

```
require('packer').startup(function()
  use 'wbthomason/packer.nvim'
  use {
    'vimwiki/vimwiki',
    config = function()
      vim.g.vimwiki_list = {
        {
          path = '~/',
          syntax = 'markdown',
          ext  = '.md',
        }
      }
      vim.g.vimwiki_ext2syntax = {
        ['.md'] = 'markdown',
        ['.markdown'] = 'markdown',
        ['.mdown'] = 'markdown',
      }
    end
  }
end)
```

## Reorganizing files
```
require("foo") -- includes ~/.config/nvim/lua/foo.lua
require("foo/bar") -- includes ~/.config/nvim/lua/foo/bar.lua
```
