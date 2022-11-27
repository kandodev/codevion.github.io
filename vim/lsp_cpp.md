This builds off of a few different concepts introduced in previous video series but the main ones are:

* [Basic Neovim LSP Setup Tutorial](https://www.youtube.com/watch?v=Ku-m7eEbWas)
* [Cmake integration in vim/neovim](https://www.youtube.com/watch?v=Y_UubM5eYAM)

After that, the plugins we use:
```
-- extra
use 'voldikss/vim-floaterm'
use 'kyazdani42/nvim-tree.lua'
use 'nvim-telescope/telescope.nvim'

-- ide
use 'neovim/nvim-lspconfig'
use 'nvim-treesitter/nvim-treesitter'
use 'williamboman/nvim-lsp-installer'
use {
  'ms-jpq/coq_nvim',
  branch = 'coq'
}
use "cdelledonne/vim-cmake'
```

Keymaps we use:
```
local keymap = vim.api.nvim_set_keymap
local opts = { noremap = true }

-- CMake
keymap('', '<leader>cg', ':CMakeGenerate<cr>', {})
keymap('', '<leader>cb', ':CMakeBuild<cr>', {})
keymap('', '<leader>cq', ':CMakeClose<cr>', {})
keymap('', '<leader>cc', ':CMakeClean<cr>', {})

-- Telescope
keymap('n', '<leader>ff', "<cmd>lua require('telescope.builtin').find_files()<cr>", opts)
keymap('n', '<leader>fg', "<cmd>lua require('telescope.builtin').live_grep()<cr>", opts)
keymap('n', '<leader>fb', "<cmd>lua require('telescope.builtin').buffers()<cr>", opts)
keymap('n', '<leader>fh', "<cmd>lua require('telescope.builtin').help_tags()<cr>", opts)

-- floaterm
vim.cmd[[let g:floaterm_keymap_toggle = '<Leader>f']]
vim.cmd[[let g:floaterm_wintype = 'split']]

-- lsp
local function nkeymap(k, map)
  vim.api.nvim_set_keymap('n', k, map, { noremap = true })
end
nkeymap('gd', ':lua vim.lsp.buf.definition()<cr>')
nkeymap('gD', ':lua vim.lsp.buf.declaration()<cr>')
nkeymap('gi', ':lua vim.lsp.buf.implementation()<cr>')
nkeymap('gw', ':lua vim.lsp.buf.document_symbol()<cr>')
nkeymap('gw', ':lua vim.lsp.buf.workspace_symbol()<cr>')
nkeymap('gr', ':lua vim.lsp.buf.references()<cr>')
nkeymap('gt', ':lua vim.lsp.buf.type_definition()<cr>')
nkeymap('K', ':lua vim.lsp.buf.hover()<cr>')
nkeymap('<c-k>', ':lua vim.lsp.buf.signature_help()<cr>')
nkeymap('<leader>af', ':lua vim.lsp.buf.code_action()<cr>')
nkeymap('<leader>rn', ':lua vim.lsp.buf.rename()<cr>')
```

LSP Configuration:
```
local function treesitter_setup()
  local configs = require'nvim-treesitter.configs'
  configs.setup {
    ensure_installed = "all", -- Only use parsers that are maintained
    ignore_install = { "phpdoc" }, -- https://github.com/claytonrcarter/tree-sitter-phpdoc/issues/15
    highlight = { -- enable highlighting
      enable = true,
    },
    indent = {
      enable = false,
    }
  }
  vim.opt.foldmethod = "expr"
  vim.opt.foldexpr = "nvim_treesitter#foldexpr()"
end

local function lsp_setup()
  local lsp_installer = require("nvim-lsp-installer")
  local coq = require "coq"

  -- tell the server the capability of foldingRange
  -- nvim hasn't added foldingRange to default capabilities, users must add it manually
  local capabilities = vim.lsp.protocol.make_client_capabilities()
  capabilities.textDocument.foldingRange = {
    dynamicRegistration = false,
    lineFoldingOnly = true
  }

  lsp_installer.on_server_ready(function(server)
    local opts = {
      capabilities = capabilities
    }
    server:setup(coq.lsp_ensure_capabilities(opts)
  end)

  vim.cmd[[let g:cmake_link_compile_commands = 1]]
end

treesitter_setup()
lsp_setup()
```

Finally, when these are set up, run:
```
:LspInstall ccls
```
And 
```
:COQdeps
```
To have coq run on buffer open, add: 
```
vim.cmd[[:COQnow -s]]
``` 

And that should be it!
