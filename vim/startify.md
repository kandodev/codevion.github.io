## vim-startify
* Install [vim-startify](https://github.com/mhinz/vim-startify): `Plug 'mhinz/vim-startify'`
* Bookmarks: 

``` 
let g:startify_bookmarks = [
  \ { 'z': '~/.zshrc' },
  \ { 'v': '~/.config/nvim/init.vim' },
  \ { 'w': '/tmp/vimwiki' },
  \ ]
```
* Use an ASCII generator for a header: http://www.network-science.de/ascii/ and then add it like so:

```
let g:startify_custom_header = [
  \ '                 .___          .__               ',
  \ '  ____  ____   __| _/_______  _|__| ____   ____  ',
  \ '_/ ___\/  _ \ / __ |/ __ \  \/ /  |/  _ \ /    \ ',
  \ '\  \__(  <_> ) /_/ \  ___/\   /|  (  <_> )   |  \',
  \ ' \___  >____/\____ |\___  >\_/ |__|\____/|___|  /',
  \ '     \/           \/    \/                    \/ ',
  \]
```

* Or do not enter for the default cow fortune thingy. Can enable unicode on it:

```
let g:startify_fortune_use_unicode = 0`
```

* Configure which lists of things you want showing up:

```
let g:startify_lists = [
      \ { 'header': ['   Bookmarks'],       'type': 'bookmarks' },
      \ { 'header': ['   MRU'],            'type': 'files' },
      \ { 'header': ['   MRU '. getcwd()], 'type': 'dir' },
      \ ]
```

* A keybinding to allow running it even after launch:

```
nmap <c-n> :Startify<cr>
```
