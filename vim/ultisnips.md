# Ultisnips
* https://github.com/SirVer/ultisnips
* Provides some common snippets: https://github.com/honza/vim-snippets
```
Plug 'SirVer/ultisnips'
Plug 'honza/vim-snippets'
```
* Default trigger binding is tab but can be changed.
* Split veritcally when opened: `let g:UltiSnipsEditSplit="vertical"`
* When you 

## Snippets
* Trigger completion with a keyword. Simple snippet 
```
snippet <keyword> "description" b
...enter snippet stuff here
endsnippet
```
* You type in the keyword and then press tab to trigger completion (or you can change it): `let g:UltiSnipsExpandTrigger="<tab>"`
* (we'll get to the random b later)
* We can also choose where to drop our cursor in the snippet:
```
snippet inc "Header include" b
#include <$1.h>
endsnippet
```
* We can even use placeholder text
```
snippet inc "Header include" b
#include <${1:iostream}.h>
endsnippet
```
* We can have multiple places in a snippet where you need to put stuff in
```
snippet func "Function" b
void ${1:funcName}(${2: arguments})
endsnippet
```
* And then we can use `<c-b>` and `<c-z>` to go back/forth between the different entry points. Although we can rebind those:
```
let g:UltiSnipsJumpForwardTrigger="<c-b>"
let g:UltiSnipsJumpBackwardTrigger="<c-z>"
```
* The `b` is the option for when to trigger completion:
  * `b` only triggers if the keyword is at the start of the line.
  * `i` trigers it inline
  * `A` triggers automatically
* See `:help Ultisnips` for more details
