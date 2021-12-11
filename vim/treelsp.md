* What is tree sitter?
* Add using `use 'nvim-treesitter/nvim-treesitter'`
* Can be used for things like highlighting, indentation, folding. Each module needs to be explicitly enabled. We configure it like so:
```
local configs = require'nvim-treesitter.configs'
configs.setup {
  ensure_installed = "maintained", -- Only use parsers that are maintained
  highlight = { -- enable highlighting
    enable = true, 
  },
  indent = {
    enable = false, -- default is disabled anyways
  }
}
```
For folding, we can do:
```
vim.opt.foldmethod = "expr"
vim.opt.foldexpr = "nvim_treesitter#foldexpr()"
```
* There's some plugins like https://github.com/JoosepAlviste/nvim-ts-context-commentstring that allow for smarter commenting based on deeper syntax for UI related code with multiple languages in the same file, etc.

* After tree sitter, we'll install lspconfig `use 'neovim/nvim-lspconfig'`
* The thing about the lsp configuration is that it works with an LSP in the backend and then we require the ability to map that LSP's functionality to the neovim lsp config. We'll dive into how some of those work in future videos, but we'll start with a simple approach, use `use 'williamboman/nvim-lsp-installer'` instead.
* So let's set this up:
```
local lsp_installer = require("nvim-lsp-installer")
lsp_installer.on_server_ready(function(server)
    local opts = {}
    server:setup(opts)
end)
```
* Now that the installer is plugged in. We can isntall a language using `:LSPInstall lua`, etc.
* Finally, before we can start using it, let's set up some keymaps:
```
nkeymap('gd', ':lua vim.lsp.buf.definition()<cr>')
nkeymap('gd', ':lua vim.lsp.buf.declaration()<cr>')
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
* Now you have to understand that each language server may or may not support all these features. But we'll start seeing diagnostics at least.
* A bit annoying to see 'undefined global' on neovim lua files, let's fix that by adding some configuration to the opts in on_server_ready:
```
    if server.name == "sumneko_lua" then
      opts = {
        settings = {
          Lua = {
            diagnostics = {
              globals = { 'vim', 'use' }
            },
            --workspace = {
              -- Make the server aware of Neovim runtime files
              --library = {[vim.fn.expand('$VIMRUNTIME/lua')] = true, [vim.fn.expand('$VIMRUNTIME/lua/vim/lsp')] = true}
            --}
          }
        }
      }
    end
```
* A few quirks I've noticed, pressing `esc` or `ctrl+[` tends to trigger immediate updates, but `ctrl+c` does not
* Working keymaps:
  * `Shift+K` to see definition. Especially useful when looking at lua objects
  * `gr` to see references
  * `gt` to see type definition
  * `\rn` to rename


