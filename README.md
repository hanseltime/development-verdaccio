# dev-verdaccio

This is an example repository for starting out with a local development verdaccio registry on your local computer.

What does this do for you?

* Publish npm modules to a non-public registry for sanity testing
* Consume published npm modules version from the local registry to verify it works on import

# Getting Started

## Install npmrc tool

```bash
    npm install -g npmrc
```

## Make a local profile that points to verdaccio

```bash
npmrc -c local
```

## Run the verdaccio server

```bash
npm server
```

## Sign in to the verdaccio server once it's running, and add it as your standard config

```bash
npm adduser --registry http://localhost:4873/
npm config set registry http://localhost:4873/
```

## Understanding the files

This folder is literally it's own contained verdaccio implementation.  The following files/directories are:

* config.yaml

    [Verdaccio configuration file](https://verdaccio.org/docs/configuration/) with suitable defaults for getting started 

* storage

    This is where verdaccio will store its published packages.  Deletion of these packages will remove them from the registry.

* htpasswd

    This is the password file that is generated when you log into this registry with:

    ```bash
    npm adduser --registry http://localhost:4873/
    ```

## Publishing a local package

If you've set up your npmrc local and logged in to this repo, then you should be able to publish
right away to the verdaccio repo when it's running.

```bash
# From your local project repo
npmrc local

yarn publish
```

Now you should be able to see the new module in the verdaccio web UI, and in the storage folder!

As long as you keep your npmrc set to local, you can also install the same package and it will pull from verdaccio.

```
yarn add my-package
```

## Clean Storage

If you would like to quickly reset the packages in your verdaccio repo, you should:

1. Stop your verdaccio instance
2. Run

    ```bash
    yarn clean-storage
    ```
