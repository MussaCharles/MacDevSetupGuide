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

## 5. ohmyzsh
- [Oh My Zsh](https://ohmyz.sh/) is an open source, community-driven framework for managing your zsh configuration.
- There are various ways to install this but, I used `curl` by running the following command on my iterm : - 
     ```bash
     sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
     ```
- After installation follow [instructions here](https://github.com/ohmyzsh/ohmyzsh#using-oh-my-zsh) on how to take full advantage of it.   
     
