---
title: "HTTP Remote"
description: "Read only remote for HTTP servers"
date: "2017-06-19"
---

<i class="fa fa-globe"></i> HTTP
-------------------------------------------------

The HTTP remote is a read only remote for reading files of a
webserver.  The webserver should provide file listings which rclone
will read and turn into a remote.  This has been tested with common
webservers such as Apache/Nginx/Caddy and will likely work with file
listings from most web servers.  (If it doesn't then please file an
issue, or send a pull request!)

Paths are specified as `remote:` or `remote:path/to/dir`.

Here is an example of how to make a remote called `remote`.  First
run:

     rclone config

This will guide you through an interactive setup process:

```
No remotes found - make a new one
n) New remote
s) Set configuration password
q) Quit config
n/s/q> n
name> remote
Type of storage to configure.
Choose a number from below, or type in your own value
 1 / Amazon Drive
   \ "amazon cloud drive"
 2 / Amazon S3 (also Dreamhost, Ceph, Minio)
   \ "s3"
 3 / Backblaze B2
   \ "b2"
 4 / Dropbox
   \ "dropbox"
 5 / Encrypt/Decrypt a remote
   \ "crypt"
 6 / FTP Connection
   \ "ftp"
 7 / Google Cloud Storage (this is not Google Drive)
   \ "google cloud storage"
 8 / Google Drive
   \ "drive"
 9 / Hubic
   \ "hubic"
10 / Local Disk
   \ "local"
11 / Microsoft OneDrive
   \ "onedrive"
12 / Openstack Swift (Rackspace Cloud Files, Memset Memstore, OVH)
   \ "swift"
13 / SSH/SFTP Connection
   \ "sftp"
14 / Yandex Disk
   \ "yandex"
15 / http Connection
   \ "http"
Storage> http
URL of http host to connect to
Choose a number from below, or type in your own value
 1 / Connect to example.com
   \ "https://example.com"
url> https://beta.rclone.org
Remote config
--------------------
[remote]
url = https://beta.rclone.org
--------------------
y) Yes this is OK
e) Edit this remote
d) Delete this remote
y/e/d> y
Current remotes:

Name                 Type
====                 ====
remote               http

e) Edit existing remote
n) New remote
d) Delete remote
r) Rename remote
c) Copy remote
s) Set configuration password
q) Quit config
e/n/d/r/c/s/q> q
```

This remote is called `remote` and can now be used like this

See all the top level directories

    rclone lsd remote:

List the contents of a directory

    rclone ls remote:directory

Sync the remote `directory` to `/home/local/directory`, deleting any excess files.

    rclone sync remote:directory /home/local/directory

### Read only ###

This remote is read only - you can't upload files to an HTTP server.

### Modified time ###

Most HTTP servers store time accurate to 1 second.

### Checksum ###

No checksums are stored.

### Usage without a config file ###

Since the http remote only has one config parameter it is easy to use
without a config file:

    rclone lsd --http-url https://beta.rclone.org :http:
