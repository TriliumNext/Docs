# Manual-server-installation
This page describes manually installing Trilium on your server. **Note that this is a not well supported way to install Trilium, problems may appear, information laid out here is quite out of date. It is recommended to use either Docker or packaged build installation.**

Requirements
------------

Trilium is a node.js application. Supported (tested) version of node.js is latest 14.X.X and 16.X.X. Trilium might work with older versions as well.

You can check your node version with this command (node.js needs to be installed):

```text-plain
node --version
```

If your Linux distribution has only an outdated version of node.js, you can take a look at the installation instruction on node.js website, which covers most popular distributions.

### Dependencies

There are some dependencies required. You can see command for Debian and its derivatives (like Ubuntu) below:

```text-plain
sudo apt install libpng16-16 libpng-dev pkg-config autoconf libtool build-essential nasm libx11-dev libxkbfile-dev
```

Installation
------------

### Download

You can either download source code zip/tar from [https://github.com/TriliumNext/Notes/releases/latest\]\]](https://github.com/TriliumNext/Notes/releases/latest%5D%5D) %%{WARNING}%%or clone git repository **from stable branch** with

```text-plain
git clone -b stable https://github.com/zadam/trilium.git %%{WARNING}%%
```

Installation
------------

```text-plain
cd trilium

# download all node dependencies
npm install

# make sure the better-sqlite3 binary is there
npm rebuild

# bundles & minifies frontend JavaScript
npm run webpack
```

Run
---

```text-plain
cd trilium

# using nohup to make sure trilium keeps running after user logs out
nohup TRILIUM_ENV=dev node src/www &
```

The application by default starts up on port 8080, so you can open your browser and navigate to [http://localhost:8080](http://localhost:8080) to access Trilium (replace "localhost" with your hostname).

TLS
---

Don't forget to [configure TLS](TLS-configuration.md) which is required for secure usage!