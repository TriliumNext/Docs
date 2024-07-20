# Upgrading TriliumNext

This document outlines the steps required to upgrade TriliumNext to a new release version.

## How to Upgrade

TriliumNext does not support built-in automatic upgrades; all updates must be performed manually. The upgrade process varies depending on the installation method:

- **[Docker Server Installation](docker-server-installation.md)**: Pull the new image and restart the container.
- **Other Installations**: Download the latest version from the [release page](https://github.com/TriliumNext/Notes/releases/latest) and replace the existing application files.

## Database Compatibility and Migration

Upon startup, TriliumNext will automatically migrate the [database](database.md) to the new version. Note that after migration, older versions of Trilium will be unable to read the database. If you need to revert to a previous version of TriliumNext and its database, you can restore the [backup](backup.md) that is created prior to migration.

## Sync Compatibility

The [synchronization](synchronization.md) protocol used by TriliumNext is versioned, requiring all members of the sync cluster to use the same protocol version. Therefore, when upgrading to a new version, you may need to upgrade all instances in the sync cluster. Changes to the sync protocol version are typically indicated on the release page.
