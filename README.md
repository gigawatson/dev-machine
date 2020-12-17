# Mac Dev Machine Setup

1. Install [Fira Code](https://github.com/tonsky/FiraCode) font.
1. Install [iTerm2](https://iterm2.com/index.html).
    - **Minimal** theme.
	- Set font to _FiraCode / Light / 16pt / 131 / Use ligatures_
	- Remove "last login time" message: `touch .hushlogin`
1. Install [Oh My ZSH](https://ohmyz.sh).
    - Install [`zsh-autosuggestions`](https://github.com/zsh-users/zsh-autosuggestions).
		- Enable tab-completion suggestions: `echo "ZSH_AUTOSUGGEST_STRATEGY=(history completion)" > ~/.oh-my-zsh/custom/zsh-autosuggestions-config.zsh`
1. Install [Homebrew](https://brew.sh).
	- `brew install php`
	- `brew install mysql`
	- `brew install git`
1. Install [Composer](https://getcomposer.org).
	- Globally: `mv composer.phar /usr/local/bin/composer`
	- Add the Composer vendor bin directory to `$PATH`: 
		- `sudo vim /etc/paths`
		- Add `/Users/{username}/.composer/vendor/bin`
1. Install the [Laravel](https://laravel.com) Installer globally:
	- `composer global require laravel/installer`
1. Install Laravel Valet globally:
	- `composer global require laravel/valet`
	- Create a code directory: `mkdir code`
	- Install Laravel Valet: `valet install`
	- Register the directory: `valet park`
1. Install [Nova](https://nova.app).
	- **Neon** theme.
	- Set font to _FiraCode / Light / 15pt / 1.75_
1. Install [GitHub Desktop](https://desktop.github.com).
1. Generate SHH key with passphrase (using GitHub instructions)
	- Backup secret key and passphrase
	- Add the SSH key to the ssh-agent
	- Add SSH key to GitHub
1. Install [GPG Suite](https://gpgtools.org) (without GPG Mail)
	- Create a new key pair
	- Backup secret key and passphrase
	- Add GPG key to GitHub
	- Tell Git to use GPG and the new signing key (globally)
		- `git config --global commit.gpgsign true`
		- `git config --global user.signingkey {SIGNING_KEY}`
1. Make stuff!
