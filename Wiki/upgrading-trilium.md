# Upgrading Trilium
Topic of this page is upgrading Trilium from one version to another.

How to upgrade
--------------

Trilium does not have a built-in auto upgrade - all upgrades have to be done manually. How to do this depends on the installation method:

*   for [docker server installation](docker-server-installation.md) - pull the image of the newer version and restart
*   for all others you need to download new version of the release artifact of your choice from the [release page](https://github.com/TriliumNext/Notes/releases/latest) and replace existing version of the application - i.e. rename/delete the old directory and extract the archive of the new version

Document compatibility and migration
------------------------------------

During Trilium startup, [database](database.md) will be checked whether it conforms to the version supported by the application. In case the document is in the old version, Trilium will automatically migrate it to the new version. This will then mean that the document will not be readable anymore by the older versions of Trilium. In case you want to go back to the old version of the document and Trilium, you can restore the [backed up](backup.md) `backup-before-migration.db` which is created before every migration.

Sync compatibility
------------------

[Synchronization](synchronization.md) protocol is versioned and all members of the sync cluster need to talk in the same protocol version. Therefore, when you are upgrading from one version to another, it might be necessary to upgrade all instances in the cluster.

Change in protocol version is usually indicated on a release page.
