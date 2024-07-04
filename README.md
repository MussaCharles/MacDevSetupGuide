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
        name = <your name>
        email = <your email>
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

- Note you might need to set git credentials using github access token. Below is the method I normally use to do so globally as described below. 

 - Step 1: 
 ```shell
 git config --global credential.helper
 ```

 - Step 2:
```shell
git config --global --unset credential.helper
``` 
- Step 3: 
```shell
git config --global credential.helper osxkeychain
```

After the three steps above you can try an of the git commands such as git pull or git clone, you should be prompted to enter your access token. Follow the instructions on Github to [Create an Access Token in Github](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token).

Reference: [add-update-refresh-github-access-token-on-mac](https://gist.github.com/jonjack/bf295d4170edeb00e96fb158f9b1ba3c)


## Automatically create git remote branch if it doesn't exist.
```shell
git config --global push.autoSetupRemote simple

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

## 20. rbenv
A ruby [version manager](https://github.com/rbenv/rbenv). Useful when you are working with tools such as [fastlane](https://docs.fastlane.tools/) which are heavily relying on a certain version of ruby. 

### Installation
```ruby
brew install rbenv ruby-build
```

Then add the following in `.zhrc` file to lLoad rbenv automatically.
```ruby
eval "$(rbenv init - zsh)"
```

### Suggested build enviroment
Before doing anything with `rbevn` the following setup are [recommended](https://github.com/rbenv/ruby-build/wiki#suggested-build-environment) 

> If you haven't done so, install Xcode Command Line Tools (`xcode-select --install`) and [Homebrew](#1-homebrew)

> For Ruby versions 2.x–3.0:
>```ruby
> brew install openssl@1.1 readline libyaml gmp
> export RUBY_CONFIGURE_OPTS="--with-openssl-dir=$(brew --prefix openssl@1.1)"
>```

> Ruby 3.1 and above requires OpenSSL 3:
> ```ruby
> brew install openssl@3 readline libyaml gmp
> export RUBY_CONFIGURE_OPTS="--with-openssl-dir=$(brew --prefix > openssl@3)"
> ```

**IMPORTANT:** In order to be able to use the installed openssl 3 certificate, `brew` gave gave the folowing suggestion. 

<details>
<summary> brew suggestion </summary>

```ruby
==> Caveats
A CA file has been bootstrapped using certificates from the system
keychain. To add additional certificates, place .pem files in
  /opt/homebrew/etc/openssl@3/certs

and run
  /opt/homebrew/opt/openssl@3/bin/c_rehash

openssl@3 is keg-only, which means it was not symlinked into /opt/homebrew,
because macOS provides LibreSSL.

If you need to have openssl@3 first in your PATH, run:
  echo 'export PATH="/opt/homebrew/opt/openssl@3/bin:$PATH"' >> ~/.zshrc

For compilers to find openssl@3 you may need to set:
  export LDFLAGS="-L/opt/homebrew/opt/openssl@3/lib"
  export CPPFLAGS="-I/opt/homebrew/opt/openssl@3/include"
```
</details>
<br>

 I had to follow what homebrew suggested at the end of installation to make commands which rely on the installed certs to work. 

 In `.zshrc` file add the following. 
 ```ruby
 # Installed openssl version 3, with command -> brew install openssl@3 readline libyaml gmp
# Got errors suggesting to add the following setups.
export PATH="/opt/homebrew/opt/openssl@3/bin:$PATH"
# Enable compilers to find openssl@3.
export LDFLAGS="-L/opt/homebrew/opt/openssl@3/lib"
export CPPFLAGS="-I/opt/homebrew/opt/openssl@3/include"
 ```


> Using RUBY_CONFIGURE_OPTS to link to a specific OpenSSL installation like suggested above is not a strict requirement for installing Ruby on macOS, but it will speed up your Ruby installation and avoid any OpenSSL compilation issues.

> Ruby 3.2 and above requires the Rust compiler if you want to have [YJIT](https://github.com/ruby/ruby/blob/master/doc/yjit/yjit.md) enabled:
> 
> ```ruby
> brew install rust
> ```
      
> Ruby 3.2.0-dev and above (only `-dev` versions) require Bison 3+:
> ```ruby
> brew install bison
> ```

Finally to install ruby versions follow [Installing Ruby versions](https://github.com/rbenv/rbenv#installing-ruby-versions) guideline. 

TR/DR
```ruby
# Example to install ruby version 3.1.3
rbenv install 3.1.3

# After installation run the following to set global rbenv ruby version
rbenv global 3.1.3
```


## 21: Fastlane
[Fastlane](https://github.com/fastlane/fastlane) is useful for automating almost everything from development/release certificates generation to testing and releasing your app. 

### Setup
The following are an easy to follow setup guidelines. 

### 1. Xcode commandline tools
```ruby
xcode-select --install
```

### 2. Install fastlane using homebrew
This is the quickest way as it doensn't need you to separately install and manage ruby versions. 
Simply run the following command. 
```ruby
brew install fastlane
```

### 3. Set up environment variables
The following are instructions based on official [documentation section](https://docs.fastlane.tools/getting-started/ios/setup/#:~:text=Set%20up%20environment,the%20following%20lines%3A) about setting enviroment variables. 

> fastlane requires some environment variables set up to run correctly. In particular, having your locale not set to a UTF-8 locale will cause issues with building and uploading your build. 
> 
> In your `~/.zshrc` add the following lines:
> ```ruby
> export LC_ALL=en_US.UTF-8
> export LANG=en_US.UTF-8
> ```


For making tools like [`update_fastlane`](https://docs.fastlane.tools/actions/update_fastlane/) action to work the following extra enviroment variables need to be set. 

> ```ruby
> export GEM_HOME=~/.gems
> export PATH=$PATH:~/.gems/bin
> ```

### Advanced Option (Recommended)
The following steps are more advanced as they involve extra configurations for ruby version and installing [bundler](https://bundler.io/guides/getting_started.html). 

---
### 4. Ruby
Fastlane uses ruby so installing ruby is needed however you can also use system ruby but it is [not recommended](https://docs.fastlane.tools/getting-started/ios/setup/#:~:text=Ruby%20is%20not%20recommended.). 

👉 Follow  [rbenv installation guidelines above](#20-rbenv) to install managed ruby. As noted in the official [fastlane documentation](https://docs.fastlane.tools/getting-started/ios/setup/) supported ruby versions are 2.5+. 


### 5. Bundler

According to the [official documentation](https://bundler.io/guides/getting_started.html)
 > Bundler provides a consistent environment for Ruby projects by tracking and installing the exact gems and versions that are needed.

 From [fastlane docs](https://docs.fastlane.tools/getting-started/ios/setup/#:~:text=It%20is%20recommended%20that%20you%20use%20Bundler%20and%20Gemfile%20to%20define%20your%20dependency%20on%20fastlane.%20This%20will%20clearly%20define%20the%20fastlane%20version%20to%20be%20used%20and%20its%20dependencies%2C%20and%20will%20also%20speed%20up%20fastlane%20execution.)

 > It is recommended that you use `Bundler` and `Gemfile` to define your dependency on fastlane. This will clearly define the fastlane version to be used and its dependencies, and will also speed up fastlane execution.
 > - Install Bundler by running gem install bundler
> - Create a `./Gemfile` in the root directory of your project with the content
> ```ruby
> source "https://rubygems.org"
> gem "fastlane
>```
> - Run bundle update and add both the `./Gemfile` and the `./Gemfile.lock` to version control
> - Every time you run `fastlane`, use `bundle exec fastlane [lane]`
> - On your CI, add bundle install as your first build step
> - To update fastlane, just run `bundle update fastlane`

### Initilize fastlane for a project
To set up a project and start using fastlane right away nagivate to the project root directory and simply run the following command. 

```ruby
fastlane init
```

Lastly follow instructions on [What's next?](https://docs.fastlane.tools/getting-started/ios/setup/#:~:text=distribute%20your%20app.-,What%27s%20next%3F,-fastlane%20created%20all) section on the official [setup documentation page](https://docs.fastlane.tools/getting-started/ios/setup/). 


## 22. onefetch
> [onefetch](https://github.com/o2sh/onefetch) is a Command-line Git information tool. It is useful if you want to show project stats, such as development languages, lines of code etc.

Installation
```shell
brew install onefetch
```

Usage
```shell
> cd /path/of/your/repo
> onefetch
```

## 23. Multiliner
> [An Xcode source extension to expand lengthy lines.](https://github.com/aheze/Multiliner)

```swift
func sum(num1: Int, num2: Int, num3: Int) {..} 

// Will be changed to
sum(
num1: Int,
num2: Int,
num3: Int
) {..}
```

> Works with Initilizers, functions array & swiftUI modifiers.

### Installation
```ruby
brew install hkamran80/things/multiliner
```

For more details, see [Multiliner offical github repo](https://github.com/aheze/Multiliner)


## 24. OpenSim
A tool which helps to deal with simulator folders. Useful to debug things like on device storage in Library folders etc.

### Installation
```ruby
 brew install opensim --cask
```

For more detals, see [OpenSim official github repo](https://github.com/luosheng/OpenSim)