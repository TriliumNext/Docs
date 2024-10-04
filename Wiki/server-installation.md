# Server Installation

This guide outlines the steps to install Trilium on your own server. You might consider this option if you want to set up [synchronization](synchronization.md) or use Trilium in a browser - accessible from anywhere.

## Installation Options

There are several ways to install Trilium on a server, each with its own advantages:

- **Recommended**: [Docker Installation](docker-server-installation.md) - Available for **AMD64** and **ARM** architectures.
- [Packaged Server Installation](packaged-server-installation.md)
- [Paid Hosting Service](https://trilium.cc/paid-hosting) - A third-party service that hosts a Trilium instance for you.
- [Manual Installation](manual-server-installation.md)
- [Kubernetes](kubernetes-server-installation.md)
- [Cloudron](https://www.cloudron.io/store/com.github.trilium.cloudronapp.html)
- [HomelabOS](https://homelabos.com/docs/software/trilium/)
- [NixOS Module](nixos-server-installation.md)

The server installation includes both web and [mobile frontends](mobile-frontend.md).

## Configuration

After setting up your server installation, you may want to configure settings such as the port or enable [TLS](tls-configuration.md). Configuration is managed via the Trilium `config.ini` file, which is located in the [data directory](data-directory.md) by default. To begin customizing your setup, copy the provided `config-sample.ini` file with default values to `config.ini`.

### Config Location

By default, `config.ini`, the [database](database.md), and other important Trilium data files are stored in the [data directory](data-directory.md). If you prefer a different location, you can change it by setting the `TRILIUM_DATA_DIR` environment variable:

```sh
export TRILIUM_DATA_DIR=/home/myuser/data/my-trilium-data
```

### Disabling Authentication

If you are running Trilium on localhost only or if authentication is handled by another component, you can disable Trilium’s authentication by adding the following to `config.ini`:

```ini
[General]
noAuthentication=true
```

## Reverse Proxy Setup

To configure a reverse proxy for Trilium, you can use either **nginx** or **Apache**.

### nginx

Add the following configuration to your `nginx` setup to proxy requests to Trilium:

```nginx
location /trilium/ {
    proxy_pass http://127.0.0.1:8080/;
    proxy_http_version 1.1;
    proxy_set_header Upgrade $http_upgrade;
    proxy_set_header Connection 'upgrade';
    proxy_set_header Host $host;
    proxy_cache_bypass $http_upgrade;
}
```

To avoid limiting the size of payloads, include this in the `server {}` block:

```nginx
# Set to 0 for unlimited. Default is 1M.
client_max_body_size 0;
```

### Apache

For an Apache setup, refer to the [Apache proxy setup](apache-proxy-setup.md) guide.
