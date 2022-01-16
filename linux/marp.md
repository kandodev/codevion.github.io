# Markdown based presentations in linux environments

_@codevion_

---

## Why
* Can be edited fully in a terminal
* universal format
* Don't need to use proprietary bloated software to present some text and images.

---

## Marp
* Fully open source.
* CLI tool for usage in terminal
* Converts from markdown into html or pdf (or even pptx if necessary)
* Converted HTML has a presentation mode
* Install using `sudo npm install -g @marp-team/   marp-cli` or by downloading from the releases page on their github https://github.com/marp-team/marp-cli

---
## Format
Quite simple
```
# Slide 1
Stuff in slide
* Normal markdown format
* Can __bold__ and _italize_ too.
---
# Slide 2
Something else
![Even images](apple.jpg)
```
---
* Converts to:
![bg right:60% 80%](blah.png)
---
## Watch Mode
* Can use `marp test.md --watch` to enable watch mode where saved changes to the markdown file are immediately converted.
* I edited this while presenting the slide
* Changes

---
## Zathura
* Opening a browser to show a presentation is still ugly.
* Zathura (https://pwmt.org/projects/zathura/) is a minimalistic pdf viewer
* Convert to pdf: `marp test.md --pdf --watch`
* Display the pdf using zathura: `zathura test.pdf`
* Use `F5` to enter presentation mode
* Can use `Space` and `Shift + Space` to go back and forth

---
## Theming
* Fully customizable with html/css
* Best bet is to take an existing theme like the dracula theme: https://github.com/dracula/marp
* Then you can run it `marp marp.md --theme marp/dracula/dracula.css  --allow-local-files --watch --pdf`
* You can just change the main colors at the top to match a different theme
* PS: I uploaded my [gruvbox_marp.css](gruvbox_marp.css) file.

---
## Limitations
* Can't split into columns easily: https://github.com/marp-team/marpit/issues/137
* Note that it uses chromium to do conversions so if you want conversion to use other files (e.g: images), you need to pass in the `--allow-local-files` flag as well.

---
## Final thoughts
* The purpose is to focus on the content.
* This entire presentation is available in markdown at [codevion.github.io]()
* Like and subscribe! :heart:
