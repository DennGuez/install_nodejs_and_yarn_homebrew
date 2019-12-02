# Install NVM, NodeJS, Yarn via Homebrew

## Notice

> Move from this [Gist](https://gist.github.com/nijicha/e5615548181676873118df79953cb709)
>
> Pull request is available. Please help me contribute this one 😂.

## Prerequisites
- [Homebrew](https://brew.sh/) should be installed (Command line tools for Xcode are included).

## Getting start

### Part A: Install NVM and NodeJS

1. Install `nvm` via Homebrew
    
    $ `brew install nvm`
    
2. Add following line to your profile. (`.profile` or `.zshrc` or `.zprofile`)

    ```bash
    # NVM
    export NVM_DIR=~/.nvm
    source $(brew --prefix nvm)/nvm.sh
    ```
    
3. Close and open your terminal again.
  Or Choose one from the following command once for reload your profile. (`.profile` or `.zshrc` or `.zprofile`)
  
    Example
      - $ `source ~/.profile`
      - $ `source ~/.zshrc`
      - $ `source ~/.zprofile`
      
4. Verify `nvm` is installed

    $ `nvm --version`
    
5. Check all avaliable version by this command

    $ `nvm ls-remote`
    
6. Install NodeJS (_Recommended to install LTS version. Current LTS is Erbium_)
    
    $ `nvm install --lts=Erbium`
    
7. Check installed NodeJS in your machine.

    $ `nvm ls`
    
8. Set global nodejs version to environment.
    
    $ `nvm use default`
    
See more about `nvm` : https://github.com/creationix/nvm

### Part B: Install Yarn and Linked nvm node to Homebrew

1. Install `yarn` via Homebrew

    $ `brew install yarn`

2. Remove `node` dependencies from Homebrew

    $ `brew uninstall node --ignore-dependencies`

3. Checkout `node` in environment `$PATH` 

    $ `which node`
    
    It should be return => `/User/<your-user-name>/.nvm/versions/node/<latest-node-lts-version>/bin/node`
    
4. Checkout `brew doctor` there should show message **WARNING missing yarn dependencies**
    
    $ `brew doctor`
    
5. Create symbol link from `nvm` for `yarn` in Homebrew.

    $ `nvm current` => v12.13.0 (Latest LTS: Erbium) (This should be **Global** node version)
    
    $ `mkdir /usr/local/Cellar/node`
    
    $ `ln -s ~/.nvm/versions/node/$(nvm current)/ /usr/local/Cellar/node`

6. Overwrite `node, npm and npx` from linked `node` in `/usr/local/Cellar/node` to `/usr/local/bin/` homebrew

    $ `brew link --overwrite node`
    
7. Checkout `ls -la /usr/local/bin` to see overwrited `node, npm and npx`
    
8. Checkout `brew doctor` again. There shouldn't have **WARNING** message.

    $ `brew doctor`

9. Prevent Homebrew upgrading node version

    $ `brew pin node`

10. Enjoy ! ❤️

### Part C: To change node.js version and Re-configure Homebrew

TODO here
- [ ] Add "How to upgrade yarn in Homebrew" with an errors
    > brew upgrade
      Error: Not upgrading 1 pinned package:
      node 12.12.0
      ==> Upgrading 1 outdated package:
      yarn 1.19.0 -> 1.19.1
      Error: You must `brew unpin node` as installing yarn requires the latest version of pinned dependencies
