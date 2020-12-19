# Dev Machine Setup (Mac)

Install the [Fira Code](https://github.com/tonsky/FiraCode) font (includes nice ligatures) for use in all consoles and code editors.

Install [iTerm2](https://iterm2.com/index.html) and use the **Minimal** theme. Set the font to **FiraCode / Light / 16pt** with a **131 line height**. Adjust the cursor (blinking underline) and window size. Remove the "last login time" message in the terminal by creating `touch .hushlogin`.

Install [Oh My ZSH](https://ohmyz.sh) with the [`zsh-autosuggestions`](https://github.com/zsh-users/zsh-autosuggestions) plugin. Enable tab-completion suggestions in the plugin with `echo "ZSH_AUTOSUGGEST_STRATEGY=(history completion)" > ~/.oh-my-zsh/custom/zsh-autosuggestions-config.zsh`.

Install [Homebrew](https://brew.sh) for general package management.
- `brew install php`
- `brew install mysql`
- `brew install git`
	
Install [Composer](https://getcomposer.org) for PHP dependency management and make it available globally with `mv composer.phar /usr/local/bin/composer` once it's installed. Add the Composer vendor bin directory to `$PATH` using `sudo vim /etc/paths` and then add "/Users/{username}/.composer/vendor/bin" to the file.

Install the [Laravel](https://laravel.com) Installer globally with `composer global require laravel/installer`.

Install Laravel Valet globally with `composer global require laravel/valet`. Create a code directory to house projects in the root directory with `mkdir code`, then do `valet install` and register the directory with `valet park`.

Install the [Nova](https://nova.app) code editor and use the **Neon** theme. Set the font to **FiraCode / Light / 15pt / 1.75**. Sign-in to Panic Sync.

Install [GitHub Desktop](https://desktop.github.com), sign-in to GitHub, and pull projects into the `code` directory.

Generate a new SHH key with a passphrase (using GitHub's instructions). Add the key to the ssh-agent and to GitHub. Don't forget to backup the secret key and passphrase.

Install [GPG Suite](https://gpgtools.org) (without GPG Mail) and create a new key pair (or import on from another computer). If new, add the key to GitHub. Tell Git to use GPG and the new signing key (globally) with `git config --global commit.gpgsign true` and then `git config --global user.signingkey {SIGNING_KEY}`. Don't forget to backup the secret key and passphrase.

Install all Google fonts to `cd ~/Library/Fonts/` with `git clone https://github.com/google/fonts.git google-fonts`. Update periodically with `cd ~/Library/Fonts/google-fonts/` and `git pull`.
	
**Now go make stuff!**
