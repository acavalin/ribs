# Ruby incremental backup system

With this script you can take incremental backups of a specific folder.

It creates its backup files within the `repository-folder` by comparing
file type, size, modification time and permissions.

It stores all files stats and archives only modified files (type/size/mtime).

~~~
USAGE: ribs [switches] <repository-folder> <target-folder/device/image_file>
    -l, --list-ts                    show available restorable versions
    -b, --backup                     update the incremental backup repo
    -r, --restore                    restores the last backup version
    -R, --restore-ts TIMESTAMP       restores the specified backup version
    -g, --gzip                       use gzip instead of xz
    -G, --pigz                       use parallel gzip instead of xz
    -x, --[no-]one-file-system       don't cross filesystem boundaries        Def. true
    -p, --[no-]permissions           store files permissions (gid/uid/modes)  Def. true
    -h, --help                       display this help

Some files are automatically excluded, you can insert any additional GLOBs patterns
by wrinting them in repo_dir/exclude.yml. This is the default list:
  - /var/tmp/*
  - /var/log/*.?.gz
  - /var/backups/*.?.gz
~~~

Examples:

~~~shell
# backup a single partition system
sudo ribs -b /mnt/usb-hd/my-pc.ribs /

# backup a raspberry pi sdcard
sudo ribs -b --no-p /mnt/usb-hd/raspi.ribs/p1 /mnt/sdcard/boot
sudo ribs -b        /mnt/usb-hd/raspi.ribs/p2 /mnt/sdcard/

# restore
sudo ribs -r /mnt/usb-hd/my-pc.ribs /mnt/anothed-hd/
~~~
