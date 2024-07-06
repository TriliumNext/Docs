# TLS-configuration
TLS configuration is required for \[\[server installation\]\]. The page below describes steps to set up TLS in Trilium itself. You might also opt for TLS termination using some reverse proxy (e.g. nginx), in that case follow a [guide like this](https://www.digitalocean.com/community/tutorials/how-to-secure-nginx-with-let-s-encrypt-on-ubuntu-20-04).

First thing to do is to get a TLS certificate. You have two options:

*   Recommended - get TLS certificate signed by root certificate authority. For personal usage, the best choice is [Let's encrypt](https://letsencrypt.org). It's free, automated and easy. You can take a look at Certbot for automatic TLS setup.
*   generate your own self-signed certificate. You will have extra trouble with importing the certificate into all machines from which you connect to the server installation so this is not recommended.

Modifying config.ini
--------------------

Now that you have your certificate, we need to modify `config.ini` in the \[\[data directory\]\] so that Trilium will use it:

```text-plain
[Network]
port=8080
# true for TLS/SSL/HTTPS (secure), false for HTTP (unsecure).
https=true
# path to certificate (run "bash bin/generate-cert.sh" to generate self-signed certificate). Relevant only if https=true
certPath=/[username]/.acme.sh/[hostname]/fullchain.cer
keyPath=/[username]/.acme.sh/[hostname]/example.com.key
```

Above is only example of how this is set up on my environment when I generated the certificate using Let's encrypt acme utility. Your paths may be completely different. (Note that if you are using a Docker installation, these paths should be in a volume or other path understood by the docker container, e.g., /home/node/trilium-data/\[DIR IN DATA DIRECTORY\].)

After you set this up, you may restart Trilium and now visit the hostname with "https".

Self-signed certificate
-----------------------

If you need to use a self-signed certificate for your server instance, the desktop instance won't trust it.

Currently the only way to make this work is by disabling certificate validation by setting this environment variable (for Linux):

```text-plain
export NODE_TLS_REJECT_UNAUTHORIZED=0
trilium
```

Trilium comes with scripts to start Trilium in this mode, e.g. `trilium-no-cert-check.bat` for Windows.

\*\* Note that disabling TLS certificate validation is insecure, so do it only if you're sure you know what you're doing! \*\*
