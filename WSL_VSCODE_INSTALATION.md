# WSL INSTALL

## 1. Sprawdzamy wersję windowsa

```
Windows key + R --> wpisujemy winver

Windows 10 version 2004 Build 19041 or higher, or Windows 11
```

## 2. Uruchomiamy Windows PowerShell

```
windows key --> wpisujemy powershel --> RMB uruchom jako administrator
```

## 3. Instalujemy wsl-a

Wyświetlenie dostępnych wersji

```
wsl --list --online
```

Instalacja wybranej dystrybucji

```
wsl --install -d Ubuntu-20.04
```

Sprawdzamy czy mamy wersję wsl-a v2

```
wsl --list --verbose
```

<br>
<br>

# WINDOWS TERMINAL INSTALL

## 1. W Microsoft Store szukamu Windows Terminal i instalujemy

Po instalacji uaktalniamy ubuntu

```
sudo apt update
sudo apt dist-upgrade
```

## 2. Klikamy na ikonce chevron i wybieramy settings i default profile wybieramy Ubuntu

## 3. Ustawiamy domyślny katalog przy uruchomieniu terminala

```
cd ~
wslpath -w .
```

```
Kopiujemy ścieżkę do Settings --> Ubuntu-20.04 --> Starting directory
```

```
\\wsl$\Ubuntu-20.04\home\marmax
```

## 4. Ustawiamy czcionkę [Fura Mono Nerd](https://github.com/ryanoasis/nerd-fonts/blob/master/patched-fonts/FiraMono/Regular/complete/Fura%20Mono%20Regular%20Nerd%20Font%20Complete.otf?raw=true)

```
Settings --> Ubuntu-20.04 -->  Appearance --> Font Face --> FuraMono Nerd Font
```

<br>
<br>

# ZSH & POWERLEVEL10K

Instalacja zsh

```
sudo apt install zsh
```

musimy ustawić zsh default-owo

```
chsh -s $(which zsh)
```

Jeśli wyskoczy menu wybieramy 0

Restartujemy terminal

To verify the shell it should print /usr/bin/zsh type

```
echo $SHELL
```

Instalacja powerlevel10k

```
git clone --depth=1 https://github.com/romkatv/powerlevel10k.git ~/powerlevel10k
echo 'source ~/powerlevel10k/powerlevel10k.zsh-theme' >>~/.zshrc

```

To access the builtin configuration wizard right from your terminal type.

```
p10k configure
```

Plugins for autosuggestion and syntax highlighting

```
git clone https://github.com/zsh-users/zsh-autosuggestions.git $ZSH_CUSTOM/plugins/zsh-autosuggestions

git clone https://github.com/zsh-users/zsh-syntax-highlighting.git $ZSH_CUSTOM/plugins/zsh-syntax-highlighting
```

Otwieramy plik konfiguracyjny

```
vim ~/.zshrc
```

Find the ZSH_THME and replace it with

```
ZSH_THEME="powerlevel10k/powerlevel10k"
```

Also add this line below to use Nerd Patched fonts?

```
POWERLEVEL9K_MODE="nerdfont-complete"
```

If you want to enable auto correction then find uncomment the line by removing # from

```
#ENABLE_CORRECTION="true"
//to this
ENABLE_CORRECTION="true"
```

Now we will add plugins so scroll down a little till you find

```
plugins=(git)
```

And now add the plugins which we downloaded, like this

```
plugins=(git zsh-autosuggestions zsh-syntax-highlighting)
```

Now the last step

```
p10k configure
```

<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>

# VSCODE SETUP

## 1. INSTALL REMOTE - WSL EXTENSIONS

## 2. INSTALL COLOR THEME EXTENSION

-  Monokai Pro - filter spectrum
-  Material Icon Theme

## 3. INSTALL PRETTIER EXTENSIONS

-  Editor: Default Formatter --> Prettier
-  Editor: Format On Save --> ON

## SETTINGS

Editor: Font Family --> Cascadia Code, Fira Code
Editor: Font Size --> 18
Editor: Line Height --> 28
Editor: Word Wrap --> ON
Editor: Detect Indentation --> OFF
Editor: Tab Size --> 3
Prettier: Tab Width --> 3
Window: Zoom Level --> 0
Editor: Font Ligatures --> editor.fontLigatures": true
Editor: Smooth Scrolling --> ON

## TERMINAL

1. Terminal > Integrated: Font Family --> FuraMono Nerd Font
2. Terminal > Integrated: Font Size --> 18

3. Instalacja ZSH shell and PowerLevel10K - [LINK](https://medium.com/@shivam1/make-your-terminal-beautiful-and-fast-with-zsh-shell-and-powerlevel10k-6484461c6efb)

4. zsh-autosuggestions - [LINK](https://github.com/zsh-users/zsh-autosuggestions)

```
plugins=(git
zsh-autosuggestions
zsh-syntax-highlighting
)
```

5. Zmieniamy domyślną kolorystykę terminala z Monokai Pro w pliku settings.json

```json
"workbench.colorCustomizations": {
      "terminal.ansiBlue": "#6350b6",
      "terminal.ansiBrightBlue": "#5AD4E6",
      "editor.selectionBackground": "#535353",
      "editor.selectionHighlightBackground": "#3d3d3d",

      "[Monokai]": {
         "editor.background": "#222",
         "activityBar.background": "#181818"
      }
   },
```

## EXTENSIONS

Install:

-  Remote - SSH
-  Auto Rename Tag

Polecane:

-  Live Share
-  Quokka.js
-  Simple React Snippets
-  React Native Tools

# settings.json

```json
{
   "workbench.iconTheme": "material-icon-theme",
   "editor.fontFamily": "Cascadia Code, Fira Code",
   "editor.fontLigatures": true,
   "editor.fontSize": 18,
   "workbench.colorTheme": "Monokai Pro (Filter Spectrum)",
   "terminal.integrated.fontFamily": "FuraMono Nerd Font",
   "terminal.integrated.fontSize": 18,
   "editor.formatOnSave": true,
   "[html]": {
      "editor.defaultFormatter": "vscode.html-language-features"
   },
   "editor.defaultFormatter": "esbenp.prettier-vscode",
   "editor.renderControlCharacters": false,
   "editor.minimap.enabled": true,
   "terminal.integrated.cursorBlinking": true,
   "terminal.integrated.cursorStyle": "line",
   "terminal.integrated.cursorWidth": 2,
   "prettier.jsxSingleQuote": true,
   "prettier.singleQuote": true,
   "editor.cursorBlinking": "phase",
   "react-native.packager.port": 19000,
   "editor.lineHeight": 28,
   "editor.fontWeight": "normal",

   "workbench.colorCustomizations": {
      "terminal.ansiBlue": "#6350b6",
      "terminal.ansiBrightBlue": "#5AD4E6",
      "editor.selectionBackground": "#535353",
      "editor.selectionHighlightBackground": "#3d3d3d",

      "[Monokai]": {
         "editor.background": "#222",
         "activityBar.background": "#181818"
      }
   },
   "liveServer.settings.donotShowInfoMsg": true,
   "editor.wordWrap": "on",
   "editor.detectIndentation": false,
   "editor.tabSize": 3,
   "prettier.tabWidth": 3
}
```

# LINKS

[Install WSL2](https://www.youtube.com/watch?v=VMZH9Pj2dXw)

[Windows development setup with WSL2, ZSH, VSCode, and more](https://www.youtube.com/watch?v=oF6gLyhQDdw)

[WSL 2: Getting started](https://www.youtube.com/watch?v=_fntjriRe48&t=1s)

[Make your terminal beautiful and fast with ZSH shell and PowerLevel10K](https://medium.com/@shivam1/make-your-terminal-beautiful-and-fast-with-zsh-shell-and-powerlevel10k-6484461c6efb)

[Windows How to have a kickass terminal in Visual Studio Code](https://www.youtube.com/watch?v=Voei5KJaeIA)

[Make your WSL or WSL2 terminal awesome](https://www.youtube.com/watch?v=235G6X5EAvM)

[How to get bash shell in Windows 10](https://www.youtube.com/watch?v=cVe-OR5neuc)
