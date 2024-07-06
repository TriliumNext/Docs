# Desktop-installation
If you want to use Trilium on the desktop, download binary release for your platform from [latest release](https://github.com/TriliumNext/Notes/releases/latest), unzip the package and run `trilium` executable.

Startup scripts
---------------

There are also some other options to start Trilium:

*   `trilium-no-cert-check` - Trilium will not validate the certificates, useful e.g. when you're syncing against a sync server with self-signed certificate
    *   Alternatively you can set `NODE_TLS_REJECT_UNAUTHORIZED=0` environment variable to the Trilium process.
*   `trilium-portable` - Trilium will try to create [data directory](data-directory.md) in the trilium's directory
*   `trilium-safe-mode` - start up in "safe mode" which disables any startup scripts which might e.g. crash the application

Synchronization
---------------

If you are using a desktop instance and would like to sync with your server instance: [Synchronization](synchronization.md)
