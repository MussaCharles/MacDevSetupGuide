# MacDevSetupGuide
Steps I follow to setup every new mac for development. 


## 1. Homebrew
- The first this I do is setting up homebrew for it to act as a package manager for most of the apps/CLI tools I use in my day to day development. 
- Note: Even though homebrew require Xcode Command lines tools to be installed first you don't need to manually install them as the command to install homebrew will automatically install Xcode select tools for you if not installed already.
- The magic command needed is as follows: - 
     ```bash
     /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
     ```
- Further installation details and other guidelines can be found on the [official homebrew website](https://brew.sh/)


## 2. Xcodes App
- Note it's Xcodes notice the "s" at the end, Not Xcode. This is a cool app to speed up  Apple's Xcode download as well as maintaining multiple versions of Xcode. 
- I normally use homebrew to handle the installation process for me using the following command : - 
     ```bash
     brew install --cask xcodes
     ```
- Other details on how the app work or alternative ways to install it can be found via the following link : - 
    - [App Version](https://github.com/RobotsAndPencils/XcodesApp)
    - [Command Line Version](https://github.com/RobotsAndPencils/xcodes)

## 3. iterm2
- [iTerm2](https://iterm2.com/index.html) is a replacement for Terminal and the successor to iTerm. It works on Macs with macOS 10.14 or newer. iTerm2 brings the terminal into the modern age with features you never knew you always wanted.

     ```bash
     brew install --cask iterm2
     ```

## 4. zsh (Only if not pre-installed)
- [Zsh](https://www.zsh.org/) is a shell designed for interactive use, although it is also a powerful scripting language.
-  Before running the following command, make sure that there is no pre-installed `zsh` in your system by running `zsh --version`. 
     ```bash
     brew install zsh
     ```

## 5. zsh-syntax-highlighting
- [zsh sytanx highlighting](https://github.com/zsh-users/zsh-syntax-highlighting) provides syntax highlighting for the shell zsh. It enables highlighting of commands whilst they are typed at a zsh prompt into an interactive terminal. This helps in reviewing commands before running them, particularly in catching syntax errors.
     ```bash
     brew install zsh-syntax-highlighting
     ```
-  After running brew install command above follow the [instructions here](https://formulae.brew.sh/formula/zsh-syntax-highlighting#default) on how to activate it. 

## 6. zsh-autosuggestions
- [zsh-autosuggestions](https://github.com/zsh-users/zsh-autosuggestions) add the ability to auto-complete as you type. 
- Easily install it via homebrew as follows : - 
     ```bash
     brew install zsh-autosuggestions
     ```
- Similar to syntax highlighting to active the plugin simply add the following line at the bottom of `.zshrc` file. 
     `source /opt/homebrew/share/zsh-autosuggestions/zsh-autosuggestions.zsh`

## 7. ohmyzsh
- [Oh My Zsh](https://ohmyz.sh/) is an open source, community-driven framework for managing your zsh configuration.
- There are various ways to install this but, I used `curl` by running the following command on my iterm : - 
     ```bash
     sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
     ```
- After installation follow [instructions here](https://github.com/ohmyzsh/ohmyzsh#using-oh-my-zsh) on how to take full advantage of it.
- Just for reference the following are some of the settings in my .zshrc conf file. 
     ```bash
     #plugins
     plugins=(
     git
     )
     ```
 ## 8. Custom scripts 
 - As you can see throwing all custominizations in `.zshrc` file can get out of control as you add more scripts. To handle this situation I prefer to put all my custom alias/shortcuts into their own file.  I named this file as .customMuchabBashCommands.sh located in root folder. Then I load it as follows in `.zshrc` file.
 ```bash
     # Load from custom scripts (More about this will be explained on the future sections)
     #source ~/.customMuchabBashCommands.sh
 ```
 
 ## 9. CocoaPods
 - Even though currently Swift Package manager is continue to be adopted still there are lots of projects which are still heavily relying on [cocoapods](https://cocoapods.org/) so install it in advance. 
     ```bash
     brew install cocoapods
     ```


 
     
