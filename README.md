# Dev Machine Setup (Mac)

## Fonts

[Fira Code](https://github.com/tonsky/FiraCode) is a nice monospace font with programming ligatures for use in all consoles and code editors.

## Code Editor

Install [Nova](https://nova.app) with the following settings:

-   **Neon** theme.
-   Font set to **FiraCode / Light / 15pt / 1.75**.
-   Sign-in to Panic Sync.

## Terminal

Install [iTerm2](https://iterm2.com/index.html) with the following settings:

-   **Minimal** theme.
-   Font set to **FiraCode / Light / 16pt / 131 line height**.
-   Adjust the cursor (to blinking underline) and window size (varies).

Remove the "last login time" message in the terminal window by creating a `.hushlogin` file in the root directory.

```zsh
touch .hushlogin
```

Install [Oh My ZSH](https://ohmyz.sh) with the [`zsh-autosuggestions`](https://github.com/zsh-users/zsh-autosuggestions) plugin. To enable tab-completion suggestions in the plugin, create a new settings file with it turned on:

```zsh
echo "ZSH_AUTOSUGGEST_STRATEGY=(history completion)" > ~/.oh-my-zsh/custom/zsh-autosuggestions-config.zsh
```

Open up `~/.zshrc` and enable the following plugins: `plugins=(git zsh-autosuggestions wp-cli)`

## Package Management (Homebrew, Composer, npm)

Install [Homebrew](https://brew.sh) for general system package management with the following packages:

-   `brew install php`
-   `brew install mysql`
-   `brew install phpmyadmin`
-   `brew install git`
-   `brew install node`
-   `brew install wp-cli`

Install [Composer](https://getcomposer.org) for PHP dependency management. Once installed, make it available globally with:

```zsh
mv composer.phar /usr/local/bin/composer
```

Add the Composer vendor bin directory to `$PATH` using:

```zsh
sudo vim /etc/paths
```

Then append `/Users/{username}/.composer/vendor/bin` to the file.

## Laravel (and Valet)

Install the [Laravel Installer](https://laravel.com) globally as well as Laravel Valet with:

```zsh
composer global require laravel/installer
composer global require laravel/valet
```

Create a **project code directory** to house projects in the root directory (`~/code`) and register it with Valet so everything automatically gets its own .test URL.

```zsh
mkdir code && cd code
valet install
valet park
```

## phpMyAdmin

Configure phpMyAdmin by opening `/usr/local/etc/phpmyadmin.config.inc.php` and setting `$cfg['Servers'][$i]['AllowNoPassword']` to `true`. Add a 32 char `$cfg['blowfish_secret']` as well.

Link **phpMyAdmin** with Valet (for https://pma.test):

```zsh
cd /usr/local/share/phpmyadmin
valet link pma
valet secure pma
```

## Git (and GitHub)

Install [GitHub Desktop](https://desktop.github.com), sign-in to GitHub, and clone projects into the `~/code` directory.

Add a global `.gitignore` in the root directory and tell git about the file:

```zsh
touch .gitignore_global
git config --global core.excludesfile ~/.gitignore_global
```

Add these to `.gitignore_global`:

-   `.nova/`
-   `.DS_Store`

### SSH (and GPG)

For authenticating, generate a new SHH key with a blank passphrase (using [GitHub's instructions](https://github.com/settings/keys)). Add the key to both the ssh-agent and to GitHub. Don't forget to back up the secret key.

For signing, install [GPG Suite](https://gpgtools.org) (without GPG Mail) and create a new key pair (or import one from another computer). If new, add the key to GitHub. Don't forget to backup the secret key and passphrase.

Tell Git to use GPG and the new signing key (globally) with:

```zsh
git config --global commit.gpgsign true
git config --global user.signingkey {SIGNING_KEY}
```

## WordPress

Install a dev installation of WordPress using Laravel Valet and wp-cli:

```zsh
cd code && mkdir wp && cd wp
wp core download --skip-content
mysql.server start
wp config create --dbname=wptest --dbuser=root
wp db create
wp core install --url=wp.test --title="WP Dev" --admin_user=user --admin_password=pass --admin_email=user@email.com --skip-email
wp post delete 1 2 --force
```

**Now go make stuff!**
