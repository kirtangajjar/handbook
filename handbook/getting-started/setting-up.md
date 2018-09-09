# Setting Up
=========================

The following article will guide you to setup EasyEngine development environment. 

## Requirements

It's assumed that you've installed EasyEngine as ee installer script installs required dependencies for you, if you haven't done so, you can install easyengine as specified [here](https://github.com/EasyEngine/easyengine#installing)

Other than that, you need following tools - 

* [hub](https://github.com/github/hub) (Not required but strongly recommended).


## Setup EasyEngine repo

1. Clone EasyEngine repository

```bash
git clone git@github.com:EasyEngine/easyengine.git
```

2. Install composer dependencies

```bash
cd easyengine && composer install --prefer-source
```

3. Add alias in your .bashrc/zshrc

```bash
echo "alias ee='sudo $(pwd)/bin/ee'" >> ~/.bashrc  # Replace bashrc with zshrc if you're using zsh
```

## Steps for working on core repository

1. Follow steps in [Setup EasyEngine repo](#Setup-EasyEngine-repo)

2. Fork easyengine core repo 

```bash
hub fork  # Assuming you're in easyengine directory
```

## Steps for working on existing commands

1. Follow steps in [Setup EasyEngine repo](#Setup-EasyEngine-repo)

2. Fork the command you want to work on.

```bash
cd vendor/easyengine/<command> && hub fork
```

3. Make the changes you want and commit them to seperate branch

4. Push the branch to your repo(use `git remote -v` to checkout your remotes)

5. Submit pull request to the command either by using github UI or with `hub` command

```bash
hub pull-request
```

## Steps for creating a new command

1. Clone/Fork the [command template repository](https://github.com/EasyEngine/command-template) and rename it to the command you want to create.

2. Update the `name` and `homepage` in the `composer.json` of the  cloned repository. If the name is not updated properly then composer update/install with it will fail.

3. Update the `composer.json` in the EasyEngine core repository, add the following in `require`:

```json
"author/command-name": "dev-master"
```

Also, append the following section in the `composer.json` for development:

```json
"repositories": {
    "author/command-name": {
        "type": "path",
        "url": "path/to/your/forked/repository"
    }
}
```

Or, you can add your repository to packagist and run `composer reqiure author/command-name`.

4. Run `composer update` in the core repository after this.

5. After that, try running the default command `hello-world` given in the template, it should give a success message as below by running it from the easyengine repository root:

```bash
$ ee hello-world
Success: Hello world.
```

Note: These manual steps for setting up a new EasyEngine command will be replaced by a scaffold command.