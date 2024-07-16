# Server Installation
This pages describes installing Trilium on your own server. You might want to do this in case you want to set up [sync](synchronization.md) or you want to use it as online version of Trilium accessible from anywhere. The server installation is a fully functioning instance i.e. "web editor".

There are several options how to do this, each one with some advantage:

*   Recommended: [Docker](docker-server-installation.md) - images for **AMD64** and **ARM**
*   [Packaged server installation](packaged-server-installation.md)
*   There's a [3rd party paid service to host a Trilium instance for you](https://trilium.cc/paid-hosting)
*   [Manual installation](manual-server-installation.md)
*   [Kubernetes](kubernetes-server-installation.md)
*   [Cloudron](https://www.cloudron.io/store/com.github.trilium.cloudronapp.html)
*   [HomelabOS](https://homelabos.com/docs/software/trilium/)
*   [NixOS module](nixos-server-installation.md)

Server installation has both web and [mobile frontend](mobile-frontend.md).

Configuration
-------------

For server installations, you might want to configure e.g. port or [TLS](tls-configuration.md). This is done in the Trilium config file, by default it's in `config.ini` in the [data directory](data-directory.md). You can start creating your configuration by copying the provided `config-sample.ini` with default values to `config.ini`.

### Config location

`config.ini`, [database](database.md) and some other important Trilium data files are by default persisted in the [data directory](data-directory.md)\]\].

If this is not desired, you may change it via `TRILIUM_DATA_DIR` environment variable to some other location, e.g.:

```text-plain
export TRILIUM_DATA_DIR=/home/myuser/data/my-trilium-data
```

### Disable authentication

Among others, you can also disable authentication (in case you run on localhost only or authentication is handled by another component) by adding the following to `config.ini`:

```text-plain
[General]
noAuthentication=true
```

Reverse proxy setup
-------------------

### nginx

```text-plain
location /trilium/ {
    proxy_pass http://127.0.0.1:8080/;
    proxy_http_version 1.1;
    proxy_set_header Upgrade $http_upgrade;
    proxy_set_header Connection 'upgrade';
    proxy_set_header Host $host;
    proxy_cache_bypass $http_upgrade;
}
```

It's also advised to add following to `server {}` block to not limit size of payloads:

```text-plain
# set to 0 for unlimited. Default is 1M.
client_max_body_size 0;
```

### Apache

See [Apache proxy setup](apache-proxy-setup.md).
