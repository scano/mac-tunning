# macOS Tunning

Scripts, tunning and hacks macOS

#### Disable gatekeeper en macOs

`$ sudo spctl --master-disable`

#### Resign app on macOS
`$ codesign --sign - --force --deep /path/to/app.app`

#### Resign broken app

`$ sudo xattr -rd com.apple.quarantine /Applications/TheApp.app`

#### Disable font smothing in macOS Big Sur

```
$ defaults -currentHost write -g AppleFontSmoothing -int 0
$ defaults write -g CGFontRenderingFontSmoothingDisabled -bool NO
```

#### Disable app power managament macOS

`$ defaults write NSGlobalDomain NSAppSleepDisabled -bool YES`

#### Show startup BIOS messages en macOS

- Activar: `$ sudo nvram boot-args="-v"`
- Desactivar: `$ sudo nvram boot-args=`

#### Tunning del ZSH con OhMyZSH

Instalar desde https://ohmyz.sh/

Editar `~/.zshrc` y modicar o añadir las lineas a estos valores

```
ZSH_THEME="avit"

plugins=(git osx)

export EDITOR=nano
export VISUAL="$EDITOR"
alias ll='ls -lha'

```

#### Set Nano as default terminal editor

Editar el archivo `~/.bash_profile` o `~/.zshrc` según interprete de consola.
Añadir:

```
export EDITOR=nano
export VISUAL="$EDITOR"
```


#### Start and End key in macOS Extended Keyboards

Open a terminal:
   
```
$ cd ~/Library
$ mkdir KeyBindings
$ cd KeyBindings
$ nano DefaultKeyBinding.dict
```

Add all text:

```
{
"\UF729" = "moveToBeginningOfLine:"; /* Home */
"\UF72B" = "moveToEndOfLine:"; /* End */
"$\UF729" = "moveToBeginningOfLineAndModifySelection:"; /* Shift + Home */
"$\UF72B" = "moveToEndOfLineAndModifySelection:"; /* Shift + End */
"^\UF729" = "moveToBeginningOfDocument:"; /* Ctrl + Home */
"^\UF72B" = "moveToEndOfDocument:"; /* Ctrl + End */
"$^\UF729" = "moveToBeginningOfDocumentAndModifySelection:"; /* Shift + Ctrl + Home */
"$^\UF72B" = "moveToEndOfDocumentAndModifySelection:"; /* Shift + Ctrl + End */
}
```

#### Ajustar el comportamiento de la exploración de SMB en macOS High Sierra 10.13

  - Fuente: https://support.apple.com/es-es/HT208209
  - Acelerar la exploración en comparticiones de red: 
  `$ defaults write com.apple.desktopservices DSDontWriteNetworkStores -bool TRUE`
  - Forzar al Finder para que recopile primero todos los metadatos: 
  `$ defaults write com.apple.desktopservices UseBareEnumeration -bool FALSE`
  - Desactivar el almacenamiento en caché del directorio: 
  `$ echo "[default]" | sudo tee -a /etc/nsmb.conf echo "dir_cache_off=yes" | sudo tee -a /etc/nsmb.conf`
 
#### Flush DNS Caches

`$ sudo killall -HUP mDNSResponder;sudo killall mDNSResponderHelper;sudo dscacheutil -flushcache;`
