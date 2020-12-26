# Dev Machine Setup (Mac)

Install the [Fira Code](https://github.com/tonsky/FiraCode) font (includes nice ligatures) for use in all consoles and code editors.

Install [iTerm2](https://iterm2.com/index.html) and use the **Minimal** theme. Set the font to **FiraCode / Light / 16pt** with a **131 line height**. Adjust the cursor (blinking underline) and window size. Remove the "last login time" message in the terminal by creating `touch .hushlogin` in the root directory.

Install [Oh My ZSH](https://ohmyz.sh) with the [`zsh-autosuggestions`](https://github.com/zsh-users/zsh-autosuggestions) plugin. Enable tab-completion suggestions in the plugin with `echo "ZSH_AUTOSUGGEST_STRATEGY=(history completion)" > ~/.oh-my-zsh/custom/zsh-autosuggestions-config.zsh`. Then enable the following plugins in `.zshrc`: "plugins=(git zsh-autosuggestions wp-cli)"

Install [Homebrew](https://brew.sh) for general package management with the following packages.

-   `brew install php`
-   `brew install mysql`
-   `brew install git`
-   `brew install node`
-   `brew install wp-cli`

Install the [Nova](https://nova.app) code editor and use the **Neon** theme. Set the font to **FiraCode / Light / 15pt / 1.75**. Sign-in to Panic Sync.

Add a global `.gitignore` in the root directory with `touch .gitignore_global` and tell git about the file with `git config --global core.excludesfile ~/.gitignore_global`. Add this to `.gitignore_global`:

-   `.nova/`
-   `.DS_Store`

Install [Composer](https://getcomposer.org) for PHP dependency management and make it available globally with `mv composer.phar /usr/local/bin/composer` once it's installed. Add the Composer vendor bin directory to `$PATH` using `sudo vim /etc/paths` and then add "/Users/{username}/.composer/vendor/bin" to the file.

Install the [Laravel](https://laravel.com) Installer globally with `composer global require laravel/installer`.

Install Laravel Valet globally with `composer global require laravel/valet`. Create a code directory to house projects in the root directory with `mkdir code`, then do `valet install` and register the directory with `valet park`.

Install [GitHub Desktop](https://desktop.github.com), sign-in to GitHub, and clone projects into the `code` directory.

Generate a new SHH key with a blank passphrase (using GitHub's instructions). Add the key to the ssh-agent and to GitHub. Don't forget to back up the secret key.

Install [GPG Suite](https://gpgtools.org) (without GPG Mail) and create a new key pair (or import one from another computer). If new, add the key to GitHub. Tell Git to use GPG and the new signing key (globally) with `git config --global commit.gpgsign true` and then `git config --global user.signingkey {SIGNING_KEY}`. Don't forget to backup the secret key and passphrase.

**Now go make stuff!**
