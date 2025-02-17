# Local Development

### Install build requirements
Install Rust using [the recommended option on rust-lang.org](https://www.rust-lang.org/tools/install) (rustup).

#### Debian-based distro
```
sudo apt install git cargo libssl-dev pkg-config libpq-dev yarn curl gnupg2 espeak
# install yarn
curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add -
echo "deb https://dl.yarnpkg.com/debian/ stable main" | sudo tee /etc/apt/sources.list.d/yarn.list
sudo apt update && sudo apt install yarn
```

#### Arch-based distro
```
sudo pacman -S git cargo libssl-dev pkg-config libpq-dev yarn curl gnupg2 espeak
# install yarn (stable)
curl -o- -L https://yarnpkg.com/install.sh | bash
```

#### macOS
Install [Homebrew](https://brew.sh/) if you don't already have it installed.

Finally, install Node and Yarn.

```
brew install node yarn
```

### Get the back end source code
```
git clone https://github.com/LemmyNet/lemmy.git --recursive
# or alternatively from gitea
# git clone https://yerbamate.ml/LemmyNet/lemmy.git --recursive
```

### Build the backend (Rust)
```
cargo build
# for development, use `cargo check` instead)
```

### Get the front end source code
```
git clone https://github.com/LemmyNet/lemmy-ui.git --recursive
```

### Setup postgresql
#### Debian-based disto
```
sudo apt install postgresql
sudo systemctl start postgresql

# Either execute db-init.sh, or manually initialize the postgres database:
sudo -u postgres psql -c "create user lemmy with password 'password' superuser;" -U postgres
sudo -u postgres psql -c 'create database lemmy with owner lemmy;' -U postgres
export LEMMY_DATABASE_URL=postgres://lemmy:password@localhost:5432/lemmy
```

#### Arch-based distro
```
sudo pacman -S postgresql
sudo systemctl start postgresql

# Either execute db-init.sh, or manually initialize the postgres database:
sudo -u postgres psql -c "create user lemmy with password 'password' superuser;" -U postgres
sudo -u postgres psql -c 'create database lemmy with owner lemmy;' -U postgres
export LEMMY_DATABASE_URL=postgres://lemmy:password@localhost:5432/lemmy
```

#### macOS
```
brew install postgresql
brew services start postgresql
/usr/local/opt/postgres/bin/createuser -s postgres

# Either execute db-init.sh, or manually initialize the postgres database:
psql -c "create user lemmy with password 'password' superuser;" -U postgres
psql -c 'create database lemmy with owner lemmy;' -U postgres
export LEMMY_DATABASE_URL=postgres://lemmy:password@localhost:5432/lemmy
```

### Run a local development instance
```
cd lemmy
cargo run
```

Then open [localhost:1235](http://localhost:1235) in your browser. To reload back-end changes, you will have to rerun `cargo run`. You can use `cargo check` as a faster way to find compilation errors.

To do front end development:

```
cd lemmy-ui
yarn
yarn dev
```

and go to [localhost:1234](http://localhost:1234). Front end saves should rebuild the project.

Note that this setup doesn't include image uploads. If you want to test those, you should use the
[Docker development](docker_development.md).
