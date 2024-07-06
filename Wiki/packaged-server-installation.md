# Packaged server installation
This is essentially Trilium sources + node modules + node.js runtime packaged into one 7z file.

Steps
-----

*   ssh into your server
*   use `wget` (or `curl` or whatever) to download latest [trilium-linux-x64-server-\[VERSION\].xz](https://github.com/TriliumNext/Notes/releases/latest) %%{WARNING}%% (notice -server suffix) on your server
*   unpack the archive, e.g. using `tar -xf -d trilium-linux-x64-server-[VERSION].tar.xz`
*   `cd trilium-linux-x64-server`
*   `./trilium.sh`
*   you can open the browser and open http://\[your-server-hostname\]:8080 and you should see Trilium initialization page

The problem with above steps is that once you close the SSH connection, the Trilium process is terminated. To avoid that, you have two options:

*   Kill it (with e.g. `CTRL-C`) and run again like this: `nohup ./trilium &`.
*   Configure systemd to automatically run Trilium in the background on every boot

Configure Trilium to auto-run on boot with systemd
--------------------------------------------------

*   After downloading, extract and move Trilium:

```text-plain
tar -xvf trilium-linux-x64-server-[VERSION].tar.xz
sudo mv trilium-linux-x64-server /opt/trilium
```

*   Create the service:

```text-plain
sudo nano /etc/systemd/system/trilium.service
```

*   Paste this into the file (replace the user and group as needed):

```text-plain
[Unit]
Description=Trilium Daemon
After=syslog.target network.target

[Service]
User=xxx
Group=xxx
Type=simple
ExecStart=/opt/trilium/trilium.sh
WorkingDirectory=/opt/trilium/

TimeoutStopSec=20
# KillMode=process leads to error, according to https://www.freedesktop.org/software/systemd/man/systemd.kill.html
Restart=always

[Install]
WantedBy=multi-user.target
```

*   Save the file (CTRL-S) and exit (CTRL-X)
*   Enable and launch the service:

```text-plain
sudo systemctl enable --now -q trilium
```

*   You can now open a browser to http://\[your-server-hostname\]:8080 and you should see the Trilium initialization page.

Common issues
-------------

### Outdated glibc

```text-plain
Error: /usr/lib64/libstdc++.so.6: version `GLIBCXX_3.4.21' not found (required by /var/www/virtual/.../node_modules/@mlink/scrypt/build/Release/scrypt.node)
    at Object.Module._extensions..node (module.js:681:18)
    at Module.load (module.js:565:32)
    at tryModuleLoad (module.js:505:12)
```

If you get an error like this, you need to either upgrade your glibc (typically by upgrading to up-to-date distribution version) or use some other [server installation](server-installation.md) method.

TLS
---

Don't forget to [configure TLS](tls-configuration.md), which is required for secure usage!
