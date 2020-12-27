# Dev Machine Setup (Mac)

This is more or less in order if setting up a new dev machine. If not, prerequisites should be obvious.

## Fonts

[Fira Code](https://github.com/tonsky/FiraCode) is a nice monospace font with programming ligatures for use in all consoles and code editors.

## Code Editor

Install [Nova](https://nova.app) with the following settings:

-   **Neon** theme.
-   Font set to **FiraCode / Light / 15pt / 1.75**.
-   Sign-in to Panic Sync.
-   **Extensions**: Emmet, Prettier

## Terminal

Install [iTerm2](https://iterm2.com/index.html) for a better Shell experience with the following settings:

-   **Minimal** theme.
-   Font set to **FiraCode / Light / 16pt / 131 line height**.
-   Adjust the cursor (to blinking underline) and window size (varies).

Remove the "last login time" message in the terminal window by creating a `.hushlogin` file in the root directory.

```zsh
touch .hushlogin
```

Install [Oh My ZSH](https://ohmyz.sh) to move from Bash to to a more interactive Zsh. Also install the [`zsh-autosuggestions`](https://github.com/zsh-users/zsh-autosuggestions) plugin and to enable tab-completion suggestions, create a new settings file with it turned on:

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

Install the [Laravel Installer](https://laravel.com) globally for PHP projects as well as Laravel Valet for a fast and minimal dev environment using Nginx and DnsMasq:

```zsh
# Install Laravel Installer
composer global require laravel/installer

# Install Laravel Valet
composer global require laravel/valet
```

Create a **project code directory** to house projects in the root directory (`~/code`) and register it with Valet so top directories automatically get their own `*.test` domain.

```zsh
mkdir code && cd code
valet install
valet park
```

## phpMyAdmin

Configure phpMyAdmin by opening `/usr/local/etc/phpmyadmin.config.inc.php` and adjusting the following settings:

-   Set `$cfg['Servers'][$i]['AllowNoPassword']` to `true`.
-   Add a 32 char `$cfg['blowfish_secret']`.

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

Add these files and directories to the `.gitignore_global`:

-   `.nova/`
-   `.DS_Store`

### SSH (and GPG)

For authentication, generate a new SHH key with a blank passphrase (using [GitHub's instructions](https://github.com/settings/keys)). Add the key to both the ssh-agent and to GitHub. Don't forget to back up the secret key.

For commit signing, install [GPG Suite](https://gpgtools.org) (without GPG Mail) and create a new key pair (or import one from another computer). If new, add the key to GitHub. Don't forget to backup the secret key and passphrase.

Tell Git to use GPG and the new signing key (globally) with:

```zsh
git config --global commit.gpgsign true
git config --global user.signingkey {SIGNING_KEY}
```

## WordPress

Install a dev installation of WordPress using Laravel Valet and wp-cli:

```zsh
# Create the new directory
cd code && mkdir wp && cd wp

# Download the latest WP version
wp core download

# Start the SQL server
mysql.server start

# Create a WP config file with debug constants set
wp config create --dbname=wptest --dbuser=root --extra-php <<PHP
define( 'WP_DEBUG', true );
define( 'WP_DEBUG_LOG', true );
PHP

# Create the database
wp db create

# Use HTTPS
valet secure wp

# Install WP (adjust details)
wp core install --url=https://wp.test --title="WP Dev Playground" --admin_user=user --admin_password=pass --admin_email=user@email.com --skip-email

# Set permalinks
wp rewrite structure '/%postname%/' --category-base=topics

# Delete the sample posts
wp post delete 1 2 --force

# Delete the default plugins
wp plugin delete hello akismet

# Install and activate dev plugins
wp plugin install query-monitor user-switching --activate
```

**Now go make stuff!**
