# Setup your Window PC

## Steps Overview

1. Update windows
2. Install chocolatey
3. Install Windows Linux Subsystem
4. Install Ubuntu
5. Install VS-Code
6. Install Hyper or your fav Term
7. Install git
8. Edit hyper.js
9. Install zsh and oh-my-zsh
10. zsh Plugins
11. Generate ssh keys and add them to your Windows
12. Install fnm, node.js and npm
13. Open directories and files with command line
14. Display git branch as list

___

Optional

- install screenfetch for bash for cool logo lookup
- install cool hyper themes and plugins
- install powerline fonts

___
___

## 1. Update your windows to the latest version

You should have the latest windows updates installed. To make sure, click on  the windows-logo, type update, click on search for updates. Install any missing updates.

## 2. Install chocolatey

Click on windows-logo, type powershell, open powershell with right-click as admin.

```
$ Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))
```

```
$ choco feature enable -n allowGlobalConfirmation
```

## 3. Install Windows Linux Subsystem

In admin powershell
```
$ choco install wsl -y
```

## 4. Install Ubuntu

Open Windows Store, search for Ubuntu and install it. Open Ubuntu, will open Ubuntu bash and install a bunch of Ubuntu things. In this setup you set your linux-user and linux-password.

## 5. Install VS-Code

In admin powershell
```
$ choco install vscode
```

Open files with VS-Code directly from the terminal

- Hit WIN + R, type SystemPropertiesAdvanced and hit Enter.
- Select the button Environment variables.
- Select path in the list from the top and push the Edit button.
- Click Add, then click Browse…
- Navigate where your Sublime Text is installed, the path added should look similar to this: `C:\Program Data\chocolatey\liv\vscode`

## 6. Install Hyper or your fav Term

In admin powershell
```
$ choco install hyper
```

## 7. Install git

[Download git.exe](https://git-scm.com/download/win) and follow setup.

## 8. Edit hyper.js

- Open Hyper
- hit Ctrl + ','
- Scroll down to `shell:` and change it to `C:\\Windows\\System32\\bash.exe`
``` 
---> here >  shell: 'C:\\Windows\\System32\\bash.exe',
```
- Scroll down to `keymaps:` and add this
```
keymaps: {
      "window:devtools": "ctrl+i",
      "window:reload": "ctrl+r",
      "window:reloadFull": "ctrl+f5",
      "window:preferences": "ctrl+,",
      "window:hamburgerMenu": "alt",
      "zoom:reset": "ctrl+0",
      "zoom:in": "ctrl+=",
      "zoom:out": "ctrl+-",
      "window:new": "ctrl+n",
      "window:minimize": "ctrl+shift+m",
      "window:zoom": "ctrl+shift+alt+m",
      "window:toggleFullScreen": "f11",
      "window:close": [
        "ctrl+q",
        "alt+f4"
      ],
      "tab:new": "ctrl+t",
      "tab:next": [
        "ctrl+shift+]",
        "ctrl+alt+right",
        "ctrl+tab"
      ],
      "tab:prev": [
        "ctrl+shift+[",
        "ctrl+alt+left",
        "ctrl+shift+tab"
      ],
      "tab:jump:prefix": "ctrl",
      "pane:next": "ctrl+pageup",
      "pane:prev": "ctrl+pagedown",
      "pane:splitVertical": "ctrl+d",
      "pane:splitHorizontal": "ctrl+e",
      "pane:close": "ctrl+w",
      "editor:undo": "ctrl+z",
      "editor:redo": "ctrl+y",
      "editor:cut": "ctrl+x",
      "editor:copy": "ctrl+c",
      "editor:paste": "ctrl+v",
      "editor:selectAll": "ctrl+a",
      "editor:movePreviousWord": "ctrl+left",
      "editor:moveNextWord": "ctrl+right",
      "editor:moveBeginningLine": "Home",
      "editor:moveEndLine": "End",
      "editor:deletePreviousWord": "ctrl+backspace",
      "editor:deleteNextWord": "ctrl+del",
      "editor:deleteBeginningLine": "ctrl+home",
      "editor:deleteEndLine": "ctrl+end",
      "editor:clearBuffer": "ctrl+k",
      "editor:break": "ctrl+c",
      "plugins:update": "ctrl+u"
  },
```

## 9. Install zsh and oh-my-zsh

### Install zsh

In Hyper 
```
$ sudo apt-get install zsh -y
```

load zsh with linux bash
```
$ vim ~/.bashrc
```
in `.bashrc` add this ( to edit in vim type i )
``` js
# Launch Zsh
if [ -t 1 ]; then
	exec zsh
fi
```
to exit vim type esc and ZZ.

### Install oh-my-zsh

In Hyper
```
sh -c "$(curl -fsSL https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)" -y
```

check your `.zshrc`
```
$ vim ~/.zshrc
```
in `.zshrc` check if following like this is included ( to edit in vim type i )
``` js
# Path to your oh-my-zsh installation.
export ZSH="/home/linux-username/.oh-my-zsh"

...

source $ZSH/oh-my-zsh.sh

# User configuration
```
to exit vim type esc and ZZ.

## 10. zsh plugins

In hyper type
```
git clone https://github.com/zdharma/fast-syntax-highlighting.git \
  ${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/plugins/fast-syntax-highlighting
```

open `.zshrc`
```
$ vim ~/.zshrc
```
in `.zshrc` scroll to plugins (to edit in vim type i)
``` js
plugins=(git fast-syntax-highlighting fasd z)
```
to exit vim type esc and ZZ.

Now you see fancy syntax highlighting in Hyper while typeing and you can use cool aliases like z to jump around in your directories.

Type alias in Hyper to see all your aliases.

## 11. Generate ssh keys, and add them to your Windows

### Generate SSh key in wsl

In Hyper type
```
$ ssh-keygen -t rsa -b 4096 -C "your-git-acc@email.com"
```
follow your promp instructions.

Copy your shh-key to clipboard
```
cat /home/your-linux-user-name/.ssh/id_rsa.pub
```

[Open GitHub -> settings -> ssh andd gpg keys](https://github.com/settings/keys) hit New SSH key to add your new SSH-key.

### Add ssh key to windows

```
mkdir .ssh
cp ~/.ssh/id_rsa.pub .ssh/id_rsa.pub
cp ~/.ssh/id_rsa .ssh/id_rsa
```

## 12. Install fnm, node.js and npm

In Hyper get unzip
```
$ sudo apt-get install unzip
```
then install fnm
```
$ curl -fsSL https://github.com/Schniz/fnm/raw/master/.ci/install.sh | bash
```
then install node.js and npm
```
$ fnm install v14.15.3
```
check node and npm is installed
```
$ node -v
$ npm -v
```
Now you installed `node.js` and npm to your wsl linux hyper.

## 13. Open directories and files with command line

```
$ npm install -g wsl-open
```
open `.zshrc` add alias
```
$ alias open="wsl-open"
```

## 14. Display git branch as list

```
$ git config --global pager.branch false
```

## Congratulations now you can run you cool dev hacks on Hyper and install easy programs with choco install in powershell admin.
___

## Optional

### install screenfetch for bash for cool logo lookup

Install screenfetch
```
$ sudo apt-get install screenfetch
```
Open and edit `.bashrc`
```
$ vim ~/.bashrc
```
add screenfetch to `.bashrc`
```
screenfetch 
```

### install cool hyper themes and plugins

[Find cool Hyper plugins and themes](https://github.com/bnb/awesome-hyper)

### install powerline fonts

[Powerline fonts](https://github.com/powerline/fonts)
