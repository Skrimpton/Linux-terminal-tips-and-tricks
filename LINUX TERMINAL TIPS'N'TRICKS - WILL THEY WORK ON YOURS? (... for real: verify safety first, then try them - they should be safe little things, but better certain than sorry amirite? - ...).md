# Simple terminal and script tips
#### Only tested on Manjaro KDE using konsole 21.12.0 and zsh 5.8 (x86_64-pc-linux-gnu)
##### And some of the [shortcuts](https://github.com/Skrimpton/Guides-and-Cheatsheets/blob/main/LINUX%20TERMINAL%20TIPS'N'TRICKS%20-%20WILL%20THEY%20WORK%20ON%20YOURS%3F%20(...%20for%20real:%20verify%20safety%20first,%20then%20try%20them%20-%20they%20should%20be%20safe%20little%20things,%20but%20better%20certain%20than%20sorry%20amirite%3F%20-%20...).md#shell-keybindings) don't work on that, so there is stuff in here that might not work for you

#

[^1]:"$PWD" is a variable which holds the path of the folder where the terminal you are using is currently doing stuff from, or inside of  
—  
See what it is with:  
  echo "$PWD"  
—  
  If "$PWD" is:                    /home/Username/  
  Then the command:                mkdir lolfolder  
  ...will (attempt to) create:     /home/Username/lolfolder/</pre>  


## Shorten "if ; then ; elif ; else ; fi "-blocks
*The following examples check whether or not "$PWD" [^1] is a folder using:* ```[ -d /path/to/folder ]```
<br> *and then outputs a text — chosen by you — depending on whether or not it is, or isn't a folder<br> (hopefully it is)*


#### You can write these if-statements:

```bash
if [ -d "$PWD" ];then;echo "Yeah it is";else;echo "Hmmm... It should be";fi
```

```bash
if [ -d "$PWD" ]
then
   echo "Yeah it is"
else
   echo "Hmmm... It should be"
fi
```
#  
<b> Like this: </b>
   

```bash
[ -d "$PWD" ] && echo "ofc" || echo "lol wut"

```  
<sup> <b> *or like this:* </b> </sup>

```bash
[ -d "$PWD" ] && 
( echo "ofc" ) || 
( echo "lol wut" )
```

<b> <sup> *even like this* </b> </sup> 

   
```bash
[ -d "$PWD" ] &&
( 
  echo -e "\nofc"
  echo -e "it's only logical"
  echo -e "...get it? like spock"
  sleep .7 && echo -en "\n:"   
  sleep .5 && echo -en "'"
  sleep .4 && echo -e "D"    
   
) || (  

  echo "lol wut"

)
```
<sup> <b>note:</b> you can also use curlybrackets for the given examples, and they will return the desired values, but you shouldn't. see [refrences](https://github.com/Skrimpton/Guides-and-Cheatsheets/blob/main/LINUX%20TERMINAL%20TIPS'N'TRICKS%20-%20WILL%20THEY%20WORK%20ON%20YOURS%3F%20(...%20for%20real:%20verify%20safety%20first,%20then%20try%20them%20-%20they%20should%20be%20safe%20little%20things,%20but%20better%20certain%20than%20sorry%20amirite%3F%20-%20...).md#refrence-list-for-here-be-dragons-)

  
#### elif 
 
<sup> *Here we first check if PWD is a folder using an if-statement <br>
and then echoing something if the if-test returns true*</sup>

<sup>*The example exits in the elif-part, see the [linked](https://stackoverflow.com/a/53900466) stackoverflow response for more details* </sup>


```bash
( [ ! -d "$PWD" ] && echo -e "Not a folder..?" ) || ( [ -d "$PWD" ] && echo -e "Yeah it should be a folder" ) || echo -e ":O"   
```
 [Beejor](https://stackoverflow.com/a/53900466) 
  >Also note that ( and [ are technically commands, so whitespace is required around them.

 <sup>right way: <code>( [ -d /folder ] )</code></sup>

<sup>wrong way: <code>([-d /folder])</code></sup>

#

### Speaking of $PWD...
## Listing environment variables:

<b> Bash </b>
```bash
bind -P
```
<b> Zsh </b>
```zsh
env
```
<b> Both:
<br><sup>*will work in many shells*</sup> </b>
```bash
printenv
```
<b> One can also list predefined variables by just passing "set" without declaring any options<br><sup>*will work in many shells*</sup></b>
```bash
set   
```
<b><sup>*```set``` produces the most complete list of variables*</sup></b>
#

## Newline(s) in Terminal

#### You can add newlines in your command prompt using ALT+ENTER or ALTGR+ENTER <br>  <sup> *(...maybe. Depending on which emulator, distro and/or shell you're using)<br>BTW: it's shift+enter in windows 10 powershell</sup><br><br>Tested on konsole where it worked in zsh, but not bash (might be a settings issue I'm missing) <br> it's shift+enter on windows powershell* 

So you can write that all-too-long one-liner visually similiar to a script — with visible newlines — like God intended


![](https://user-images.githubusercontent.com/64572787/149601795-1fa07384-d534-4b51-bbfe-16477d041fe4.png)


#### Kill all background-jobs - bash aliases

*- For all jobs*

```bash

alias kill-all-jobs='thejobs=$(jobs | wc -l);[ "$thejobs" != 0 ] && while [ "$thejobs" != 0 ];do for i in "$thejobs"; do [ "$thejobs" != 0 ] && kill %$i; done; thejobs=$(jobs | wc -l); done || echo "No jobs"'

```


*- For all suspended jobs*

```bash
alias kill-all-suspended='thejobs=$(jobs -ps | wc -l);[ "$thejobs" != 0 ] && while [ "$thejobs" != 0 ];do for i in "$thejobs"; do [ "$thejobs" != 0 ] && kill %$i; done; thejobs=$(jobs -ps | wc -l); done || echo "No suspended jobs"'
```

*- Readable version - for use in a script*
```bash
#!/bin/bash
  
####### SWITCHING WHICH OF THESE TWO LINES ARE COMMENTED OUT CHANGES IT FROM SUSPENDED JOBS TO ALL BACKGROUND JOBS
####### this is determined by the -ps option of the "jobs"-command 

#thejobs=$(jobs | wc -l) 
thejobs=$(jobs -ps | wc -l)
  
###################################################################  

[ "$thejobs" != 0 ] && while [ "$thejobs" != 0 ]
  do 
    for i in "$thejobs" 
      do 
        [ "$thejobs" != 0 ] && kill %$i
      done
    thejobs=$(jobs -ps | wc -l)
  done || echo "Nothing to kill"
```

#



## Shell Keybindings
##### *(copy pasted from [2KAbhishek](https://gist.github.com/2KAbhishek/9c6d607e160b0439a186d4fbd1bd81df))*

### Navigation 🚀

Alt + f/b  - Move cursor to previous/next word <br>

Ctrl + a/e - Move cursor to beginning/end of command <br>

Ctrl + xx  - Toggle between the start of line and current cursor position <br>

---

### Editing ✏️

Ctrl + x,e   - Open command in editor <br>

Ctrl + k     - Cut till end <br>

Ctrl + u     - Delete whole line (zsh)/ cut until beginning (bash) <br>

Alt + w      - Delete until beginning (zsh) <br>

Alt + l/u    - Lowercase/Uppercase word <br>

Alt + c      - Capitalize Word <br>

Ctrl + w     - Cut previous word <br>

Alt + Del    - Delete previous word <br>

Alt + d      - Delete next word <br>

Alt +. or !$ - Previous commands last arguement <br>

!*           - All arguments of previous command <br>

Alt + t      - Swap current word with previous <br>

Ctrl + t     - Swap the last two characters before the cursor (typo). <br>

Esc + t      - Swap the last two words before the cursor <br>

Ctrl + y     - Paste <br>

Ctrl + _     - Undo <br>

Alt + r      - Cancel the changes, revert <br>

---

### Process 📊

Ctrl + l - Clear screen <br>

Ctrl + c - Interrupt/Kill <br>

Ctrl + d - Close Current Shell <br>

Ctrl + z - Background/Foreground job <br>

---

### History ⏳

Ctrl + r   - History search <br>

Ctrl + s   - Go back to the next most recent command <br>

^abc­^­def   - Run previous command, replacing abc with def <br>

---

### Modes 🕹️

Ctrl +x,v - vi mode (zsh) <br>

set -o vi - Vi mode <br>

#

#### Refrence list, for here be dragons... [﹖](https://en.wikipedia.org/wiki/Here_be_dragons)

###### *[ZSH.sourceforge.io - Alternate forms for complex commands](https://zsh.sourceforge.io/Doc/Release/Shell-Grammar.html#Alternate-Forms-For-Complex-Commands)*

###### [man7.org - BASH manual on shellgrammar (compund commands are relevant)](https://man7.org/linux/man-pages/man1/bash.1.html#SHELL_GRAMMAR)

###### [linux.com - Curly brackets](https://www.linux.com/topic/desktop/all-about-curly-braces-bash/)

###### [Stackoverflow answer from "Beejor"](https://stackoverflow.com/a/53900466)
