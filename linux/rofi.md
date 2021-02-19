* https://wiki.archlinux.org/index.php/Rofi
* Install `sudo pacman -S rofi`
* Run using `rofi -show {mode}`
* Rofi modes:
  * window: currently open windows:
    * Shift-delete to close
  * run: dmenu like way to open programs
  * ssh: quickly ssh into stuff:
    * You can add a host to your `~/.ssh/config`:
      ```
      Host blah
        HostName blahblah.blah.com
        User codevion
      ```
    * And then ssh into it using `rofi -show ssh` and selecting `blah`
* Can combine multiple modes into one view:
  * `-combi-modi window,run`
