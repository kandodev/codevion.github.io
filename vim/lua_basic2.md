# Basic Lua Configuration for Neovim - Part 2

* Based on video in https://www.youtube.com/watch?v=cAfPmPjxRQE
[](https://www.youtube.com/watch?v=cAfPmPjxRQE)

* Not worry about configuration options, just use `vim.opt` instead.
* Running any vim command inside lua:
```
vim.cmd [[colorscheme gruvbox]]
```
* Determining OS for multiplatform configuration:
```
vim.loop.os_uname().sysname == "Darwin"
```
* Also it's a bit annoying to navigate to all these configuration files manually. gf should just work.   
* Add to ~/.config/nvim/after/ftplugin/lua.lua:
```
vim.opt_local.suffixesadd:prepend('.lua')
vim.opt_local.suffixesadd:prepend('init.lua')
vim.opt_local.path:prepend(vim.fn.stdpath('config')..'/lua')
```  
* Let's also set up a startify alternative called Alpha as our startpage
```
local keymap = vim.api.nvim_set_keymap
use { 
    'goolord/alpha-nvim',
    requires = { 'kyazdani42/nvim-web-devicons' },
    config = function ()
      require'alpha'.setup(require'alpha.themes.startify'.opts)
      local startify = require("alpha.themes.startify")
      startify.section.mru_cwd.val = { { type = "padding", val = 0 } }
      startify.section.bottom_buttons.val = {
        startify.button("e", "new file", ":ene <bar> startinsert <cr>"),
        startify.button("v", "neovim config", ":e ~/.config/nvim/init.lua<cr>"),
        startify.button("q", "quit nvim", ":qa<cr>"),
      }  
      keymap('n', '<c-n>', ':Alpha<cr>', {noremap = true})
    end
  }   
```

