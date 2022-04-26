# OSMOSE SERVER #


## GETTING STARTED ##

### Redis

You need Redis server install on your computer.

#### On Linux

```
wget http://download.redis.io/redis-stable.tar.gz
tar xvzf redis-stable.tar.gz
cd redis-stable
make
```

check if redis work:

```
redis-cli ping
```

You should see **PONG** on the output

#### On Mac

```
brew install redis
```

you can launch the server with:

```
brew services start redis
```

---

### Rust

Project have dependency on Rust

#### On Linux

```
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
```

#### check

```
rustup --version
```
it should return the last version of rust

#### On Mac

```
brew install rustup
```

use rustup to install the compiler and the package manager:

```
rustup-init
```

#### check

```
rustup --version
```
it should return the last version of rust

---

### Libcurl4

an error can occur during your setup because of the libcurl package, in case you enconter it:

#### On linux

Check if package Libcurl is already on your computer:

```
dpkg -s libcurl4
```

**if not:**

```
sudo apt install libcurl4-openssl-dev
```

---

### Postgres

#### On Linux

check if postgresql if already install on your computer:

```
which psql
```

if you see no output, then run:

```
sudo apt install -y postgresql postgresql-contrib libpq-dev build-essential
```

then, you need to create a role for using psql:

```
sudo -u postgres psql --command "CREATE ROLE <YOUR_USERNAME> LOGIN createdb;"
```

#### On Mac

check if it's already installed:

```
postgres -V
```

if not:

```
brew install postgresql
brew services start postgresql
```
check the installation:

```
psql -d postgres
```

this command should return a new prompt:

```
psql (x.x)
Type "help" for help.

postgres=#
```

---

### Ruby

project is running on ruby 2.7.2
check your ruby version:

```
ruby -v
```

if your ruby version is different from '2.7.2', you'll need to install it. 
I personnaly use RBENV to manage different version of ruby, but you can do the same with RVM.

#### On Linux

##### install rbenv

check if you already have rvm installed, you have to delete it to avoid conflict:

```
rvm implode && sudo rm -rf ~/.rvm
```
if the output is something like "'rvm' command not found", don't panik it's a good thing

```
rm -rf ~/.rbenv
sudo apt install -y build-essential tklib zlib1g-dev libssl-dev libffi-dev libxml2 libxml2-dev libxslt1-dev libreadline-dev
```

then:

```
git clone https://github.com/rbenv/rbenv.git ~/.rbenv
git clone https://github.com/rbenv/ruby-build.git ~/.rbenv/plugins/ruby-build
```

**close your terminal and reopen a new one**

##### install ruby

```
rbenv install 2.7.2
```

then you need to specified your computer that 2.7.2 is the default version:

```
rbenv global 2.7.2
```

if you don't want ruby 2.7.2 has default version on your computer, you can just precise your computer that will be default version just for this project

first, enter the project directory:
```
cd path/to/project
rbenv local 2.7.2
```

**restart your terminal** and check if the config is good:

```
ruby -v
```
it should return 'ruby 2.7.2p'

#### On Mac

##### Install rbenv

check if you already have rvm installed, you have to delete it to avoid conflict:

```
rvm implode && sudo rm -rf ~/.rvm
```
if the output is something like "'rvm' command not found", don't panik it's a good thing

```
sudo rm -rf $HOME/.rbenv /usr/local/rbenv /opt/rbenv /usr/local/opt/rbenv
brew uninstall --force rbenv ruby-build
```
**Quit your terminal and open a new one**
then:

```
brew install rbenv
```

#### Install ruby

```
rbenv install 2.7.2
```

then you need to specified your computer that 2.7.2 is the default version:

```
rbenv global 2.7.2
```

if you don't want ruby 2.7.2 has default version on your computer, you can just precise your computer that will be default version just for this project

first, enter the project directory:
```
cd path/to/project
rbenv local 2.7.2
```

---

### Node

you need to have node install on your computer (v14.x)

First, I strongly advice to use a version manager like rbenv but for node.

#### NVM

##### On Linux and Mac

I have to precise that I use zsh as default terminal prompt, if you use another one, please change 'zsh' by the one you're using:

```
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.37.0/install.sh | zsh
```

**restart yout terminal**

then, check nvm:

```
nvm -v
```

it should return you a version. if not, it may be caused by the export path on your .zshrc ( or .bashrc ...)
check if the code below is present on your terminal file config:

``` 
export NVM_DIR="$([ -z "${XDG_CONFIG_HOME-}" ] && printf %s "${HOME}/.nvm" || printf %s "${XDG_CONFIG_HOME}/nvm")"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh" # This loads nvm
``` 

then, you can install the desired node version using:

```
nvm install 14.15
```

check with: 
```
node -v
```

**PS:** *you can list all available version of node installed on your computer with the following command:*

```
nvm ls
```

*and switch from a version to another one with:*

```
nvm use x.x
```

---

### Bundler

#### On linux and Mac

run:

```
gem install bundler
```

### Docker Compose

docker is used by the project to listen to mails send locally

#### On Linux


download the lastest stable release:

```
sudo curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
```

add permissions to the binary:

```
sudo chmod +x /usr/local/bin/docker-compose
```

then test:

```
docker-compose --version
```

it should return something like that:
docker-compose version 1.29.2, build 5becea4c

### Minio

Minio is an open source S3 stockage object server with a high performance.

#### Installation

##### On Linux

download the lastest stable version:

```
wget https://dl.min.io/server/minio/release/linux-amd64/minio
chmod +x minio
```

##### On Mac

```
brew install minio/stable/minio
```

#### launch a server:

MINIO_ROOT_USER and MINIO_ROOT_PASSWORD permit you to define your server saccess key and secret key, if not minio will generate them
/data is the storing directory
--console-address is the flag to define in which port minio is listening to


```
MINIO_ROOT_USER=admin MINIO_ROOT_PASSWORD=password ./minio server /data --console-address ":9001"
```

your output will be:

```
API: http://192.168.0.186:9000  http://172.17.0.1:9000  http://172.18.0.1:9000  http://127.0.0.1:9000           
RootUser: admin 
RootPass: password 

Console: http://192.168.0.186:9001 http://172.17.0.1:9001 http://172.18.0.1:9001 http://127.0.0.1:9001      
RootUser: admin 
RootPass: password
```

open the **console url** to access the server platform then create your bucket with the same name as the S3 bucket, then enter your S3 Access key and S3 Secret key, then create a user with the appropriate policy.


You're done with the setup

---

## Run Project

### the first time

#### install package
```
npm install
bundle install
```

#### Init DB

two ways:
to avoid divergence error due to existing databases:
```
rails db:drop
```
or
```
dropdb osmose_development
dropdb osmose_test
```

then create new ones:
```
rails db:create
```
it will create the two following databases: **osmose_development** and **osmose_test**

or manually:

```
createdb osmose_development
createdb osmose_test
```

and restore structure and data from staging dump:
```
pg_restore -d osmose_development path/to/filename.dump
```

### At each Pull

```
npm install
bundle install
```

### launch server

you can run the needed servers with:

```
invoker Procfile.dev
```

>The application is on http://localhost:3000.
>The mail catcher is on http://localhost:1080.

#### potential errors

you may have some error:

##### Docker

if docker doesn't start, it may be caused to the permission offer to docker compose, personnaly i use: 
```
sudo docker-compose up
```

##### Client

if client doesn't work, launch the server on an other terminal window at the **root of the project**:

```
rm app/assets/webpack/* || true && cd client && bundle exec rake react_on_rails:locale && npm run build:development
```

### Tests

you can have a console open with:

```
bundle exec guard
```
that automatically launched tests when you modify a file.

Personnaly, I rather test my code using TDD method so you can run tests with:

```
rspec spec/path/to/filename_spec.rb
```


