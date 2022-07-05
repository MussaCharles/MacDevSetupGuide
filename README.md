# MacDevSetupGuide
Recently I changed my development mac from Intel based Machine to Apple's M1 Max. Since they are two different architectures I decided to ditch Time Machine backup and start fresh on the new Chip. However I found myself having to redo the process of configuring my development environment from scratch. It's something which I did years ago on my intel based Mac as you might have guessed it's difficult to remember all the steps without searching around the web. 

To avoid going through the same route in the future every time I change to a new Machine I have decided to document all the steps. I made them public so that new devs or other senior devs can take advantage of it when needed.

Enough talking below are the steps to setup new MacBook for development.

**Disclamer:** These configurations are based on my experience as an iOS Dev so it might not work well for other fields but can be useful if your main development Machine runs MacOS.


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
 ## 7.1 ohmyzsh themes
 To set other themes than the default one See [Themes Wiki](https://github.com/ohmyzsh/ohmyzsh/wiki/Themes)
 As a reference the following is a theme which I use on my custom configuration.
 
 Inside a `.zshrc` file add the following: - 
 ```bash
 ZSH_THEME="jonathan"
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

## 10. carthage
- [Carthage](https://github.com/Carthage/Carthage) is intended to be the simplest way to add frameworks to your Cocoa application.
     ```bash
     brew install carthage
     ```
- A note about [carthage issue on M1 Macs](https://github.com/Carthage/Carthage/issues/3110). There is a known issue which happens during build phase of Xcode Project having libraries/frameworks depending on carthage. To fix this issue you need to create a symbolic link to carthage version mananged by brew. 

**Important:** Make sure you have a bin folder located in `/usr/local` first otherwise you will get an error of missing directory. 

  - Step 1: Create bin directory
  
         # assuming that you are inside /user/local folder.
          sudo mkdir bin
         
  - step 2: Create a symbolic link 
  
         sudo ln -s /opt/homebrew/bin/carthage /usr/local/bin/carthage
         


## 11. gitignore file
-  On every new project this file should be the first thing to configure. So since I work on iOS projects most of the time. I have a [common file](.gitignore) which I include in almost all iOS projects.
     ```bash
     # On every new project folder, before any new file is created run. 
     touch .gitignore
     ```
    - Then populate it with the contents of [this file](.gitignore)


## 12. GitHub CLI
- From the official [website](https://cli.github.com/manual/) GitHub CLI, or gh, is a command-line interface to GitHub for use in your terminal or your scripts.
-  To install using homebrew run the following command : - 
     ```bash
      brew install gh
     ```
- After installing make sure you follow the instructions on how to authenticate with Github so that you can quickly start working on existing projects hosted on Github.  TL,DR version of the doc, simply run the following command and follow the interactive terminal guidelines. 
     ```bash
     gh auth login
     ```

## 13. Configure Git's user name & email.
     
     git config --global --edit
    
     
  Doing so will open vim editor. Proceed by updating configurations. As a reference the following are my configurations as for the time of writing this (May 26, 2022). 
  Note that if other things don't make sense at least configure the [user] section with your name and email then google sections which you don't understand. 

 
     [filter "lfs"]
        process = git-lfs filter-process
        required = true
        clean = git-lfs clean -- %f
        smudge = git-lfs smudge -- %f
     [user]
        name = MussaCharles
        email = mussacharles50@gmail.com
     [core]
        excludesfile = ~/.gitignore_global
     [merge]
        tool = opendiff
        ff = false
      [mergetool]
        keepBackup = false
     [pager]
        branch = false
        log = true
    [pull]
        rebase = false
        ff = only
    [init]
        defaultBranch = main
        


## 14. Get up and running with your remote git projects
- Clone a git repo. This will only clone the master/main branch.
     ```bash
     git clone <remote URL>
     ```
- To work with git branches I found the following [commands](https://stackoverflow.com/a/10313379/7551807) very useful. 
     ```bash
     # To list remote branches:
     git branch -r
     
     #You can check them out as local branches with:
     
     git checkout -b LocalName origin/remotebranchname
     
     ```
     

## 15. Show Build time on Xcode
```bash
defaults write com.apple.dt.Xcode ShowBuildOperationDuration YES
```


## 16. Rectangle
- [Rectangle](https://github.com/rxhanson/Rectangle) is an opensource app which help to save a lot of time by quickly use keyboard shortcuts to move or resize windows on MacOS. It is very similar to [Spectacle](https://github.com/eczarny/spectacle) but unfortunately Spectacle is no longer maintained but it still working as I have been using on my old intel based Mac with no issues. 
- To install Rectangle simply run the following command
     ```bash
     brew install --cask rectangle
     ```
 - **Important:** there is an issue mentioned in the [official rectangle doc](https://github.com/rxhanson/Rectangle#window-resizing-is-off-slightly-for-iterm2) that iTerm2 resizing is somehow off due to it's internal restriction. Read more on the relevant link for more info. But to fix the issue simply run the following command on your terminal. 
     ```bash
       defaults write com.googlecode.iterm2 DisableWindowSizeSnap -integer 1
     ```
     
     
## 17. Git Large File Storage
From the official [site definition](https://git-lfs.github.com/) Git Large File Storage (LFS) replaces large files such as audio samples, videos, datasets, and graphics with text pointers inside Git, while storing the file contents on a remote server like GitHub.com or GitHub Enterprise.

To install run the following command

 ```bash
      brew install git-lfs
 ```

It is very easy to use this tool, simple follow the instructions on the [official website here](https://git-lfs.github.com/)


## 18. FengNiao
A command line tool for [cleaning unused resources in Xcode](https://github.com/onevcat/FengNiao). It is useful if you have a huge project or legacy project with logs of old image assets which are no longer needed. 

To install it, you need to use [Mint](https://github.com/yonaskolb/Mint), 

```bash
    brew install mint
    mint install onevcat/fengniao
```

## 19. fui
A [tool](https://github.com/dblock/fui) to help finding unused Objecitve-C imports. For those who have inherited legacy Objective-C projects. This tool can be very useful to find used legacy code as you port it to another language eg: Swift. 

Installation
```ruby
sudo gem install fui
````
      
           
      

