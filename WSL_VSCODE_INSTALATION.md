# WSL INSTALL

## 1. Sprawdzamy wersję windowsa

```
Windows key + R --> wpisujemy winver

Windows 10 version 2004 Build 19041 or higher, or Windows 11
```

<br>

## 2. Uruchomiamy Windows PowerShell

```
windows key --> wpisujemy powershel --> RMB uruchom jako administrator
```

<br>

## 3. Instalujemy wsl-a

Wyświetlenie dostępnych wersji

```
wsl --list --online
```

Instalacja wybranej dystrybucji

```
wsl --install -d Ubuntu-20.04
```

Zrestartować komputer

```
Ustawić login
Ustawić hasło
```

Sprawdzamy czy mamy wersję wsl-a v2

```
wsl --list --verbose
```

<br>

## - Możemy resetować i odinstalować ubuntu

```
Ustawienia --> Aplikacje --> Ubuntu --> Opcje zaawansowane --> Resetuj
Ustawienia --> Aplikacje --> Ubuntu --> Opcje zaawansowane --> Odinstaluj

po resecie uruchamiamy ponownie instalację
wsl --install -d Ubuntu-20.04
```

<br><br><br><br>

# WINDOWS TERMINAL INSTALL

## 1. W Microsoft Store szukamu Windows Terminal i instalujemy

Po instalacji uaktalniamy ubuntu

```
sudo apt update
```

```
sudo apt dist-upgrade
```

<br>

## 2. Klikamy na ikonce chevron i wybieramy settings i default profile wybieramy Ubuntu

<br>

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

<br>

## 4. Ustawiamy czcionkę [Fura Mono Nerd](https://github.com/ryanoasis/nerd-fonts/blob/master/patched-fonts/FiraMono/Regular/complete/Fura%20Mono%20Regular%20Nerd%20Font%20Complete.otf?raw=true)

```
Settings --> Ubuntu-20.04 -->  Appearance --> Font Face --> FuraMono Nerd Font
```

<br><br><br><br>

# ZSH & POWERLEVEL10K

## 1. Instalacja zsh

```
sudo apt install zsh
```

musimy ustawić zsh default-owo

```
chsh -s $(which zsh)
```

Restartujemy terminal

Jeśli wyskoczy menu wybieramy 0

Sprawdzamy typ shell-a powinien być /usr/bin/zsh

```
echo $SHELL
```

<br>

## 2. Instalacja powerlevel10k

```
git clone --depth=1 https://github.com/romkatv/powerlevel10k.git ~/.plugins/powerlevel10k
```

```
echo 'source ~/.plugins/powerlevel10k/powerlevel10k.zsh-theme' >>~/.zshrc
```

Restartujemy terminal i konfigurujemy powerlevel10k

Możemy ponownie zkonfigurować powerlevel10k z terminala za pomocą polecenia

```
p10k configure
```

<br>

## 3. Instalujemy pluginy do autosugesti i podświetlania (z lub bez sudo)

```
git clone https://github.com/zsh-users/zsh-autosuggestions.git ~/.plugins/zsh-autosuggestions
```

```
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ~/.plugins/zsh-syntax-highlighting
```

Dodajemy pluginy do pliku .zshrc

```
echo 'source ~/.plugins/zsh-autosuggestions/zsh-autosuggestions.zsh' >>~/.zshrc
```

```
echo 'source ~/.plugins/zsh-syntax-highlighting/zsh-syntax-highlighting.zsh' >>~/.zshrc
```

Resetujemy Terminal

<br>

## 4. Żeby otrzymać takie same kolory w zsh jak w bashu to dodajemy w .zshrc kod

```
# enable color support of ls and also add handy aliases
  if [ -x /usr/bin/dircolors ]; then
      test -r ~/.dircolors && eval "$(dircolors -b ~/.dircolors)" || eval "$(dircolors -b)"
      alias ls='ls --color=auto'
      alias dir='dir --color=auto'
      alias vdir='vdir --color=auto'
      alias grep='grep --color=auto'
      alias fgrep='fgrep --color=auto'
      alias egrep='egrep --color=auto'
  fi

# some more ls aliases
    alias ll='ls -alF'
    alias la='ls -A'
    alias l='ls -CF'
```

<br><br><br><br>

# VSCODE SETUP

## 1. INSTALL VSCODE

<br>

## 2. SETTINGS - wklejamy w settings.json

<br>

```json
{
   "editor.fontFamily": "Cascadia Code, Fira Code",
   "editor.fontLigatures": true,
   "editor.fontSize": 18,
   "editor.formatOnSave": true,
   "editor.defaultFormatter": "esbenp.prettier-vscode",
   "editor.renderControlCharacters": false,
   "editor.minimap.enabled": true,
   "editor.wordWrap": "on",
   "editor.detectIndentation": false,
   "editor.tabSize": 3,
   "editor.cursorBlinking": "phase",
   "editor.lineHeight": 28,
   "editor.fontWeight": "normal",
   "editor.smoothScrolling": true,
   "prettier.jsxSingleQuote": true,
   "prettier.singleQuote": true,
   "prettier.tabWidth": 3,
   "terminal.integrated.fontSize": 18,
   "terminal.integrated.fontFamily": "FuraMono Nerd Font",
   "terminal.integrated.cursorBlinking": true,
   "terminal.integrated.cursorStyle": "line",
   "terminal.integrated.cursorWidth": 2,
   "workbench.colorTheme": "Monokai Pro (Filter Spectrum)",
   "workbench.iconTheme": "material-icon-theme",
   "workbench.colorCustomizations": {
      "editor.selectionBackground": "#535353",
      "editor.selectionHighlightBackground": "#3d3d3d",
      "terminal.ansiBlue": "#6350b6",
      "terminal.ansiBrightBlue": "#5AD4E6",

      "[Monokai]": {
         "activityBar.background": "#181818",
         "editor.background": "#222"
      }
   }
}
```

<br>

## 3. INSTALL EXTENSIONS

### 1. REMOTE - WSL EXTENSIONS

### 2. MONOKAI PRO

-  filter spectrum

### 3. MATERIAL ICON THEME

### 4. PRETTIER EXTENSIONS

### 5. EXTENSIONS

Install:

-  Remote - SSH
-  Auto Rename Tag

Polecane:

-  Live Share
-  Quokka.js
-  Simple React Snippets
-  React Native Tools

<br><br><br><br>

# LINKS

[Install WSL2](https://www.youtube.com/watch?v=VMZH9Pj2dXw)

[Windows development setup with WSL2, ZSH, VSCode, and more](https://www.youtube.com/watch?v=oF6gLyhQDdw)

[WSL 2: Getting started](https://www.youtube.com/watch?v=_fntjriRe48&t=1s)

[Make your terminal beautiful and fast with ZSH shell and PowerLevel10K](https://medium.com/@shivam1/make-your-terminal-beautiful-and-fast-with-zsh-shell-and-powerlevel10k-6484461c6efb)

[Windows How to have a kickass terminal in Visual Studio Code](https://www.youtube.com/watch?v=Voei5KJaeIA)

[Make your WSL or WSL2 terminal awesome](https://www.youtube.com/watch?v=235G6X5EAvM)

[How to get bash shell in Windows 10](https://www.youtube.com/watch?v=cVe-OR5neuc)
