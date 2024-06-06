---
{"dg-publish":true,"permalink":"/thm-notes/linux-n/backup-and-restore/","title":"Backup And Restore -Linux","tags":["linux"]}
---

## Backup and Restore

Linux systems offer a variety of software tools for backing up and restoring data. These tools are designed to be efficient and secure, ensuring that data is protected while also allowing us to easily access the data we need.

### Backup Tools on Ubuntu

When backing up data on an Ubuntu system, we can utilize tools such as:

- Rsync
- Deja Dup
- Duplicity

#### Rsync

Rsync is an open-source tool that allows us to quickly and securely back up files and folders to a remote location. It is particularly useful for transferring large amounts of data over the network, as it only transmits the changed parts of a file. It can also be used to create backups locally or on remote servers. If we need to back up large amounts of data over the network, Rsync might be the better option.

#### Duplicity

Duplicity is another graphical backup tool for Ubuntu that provides users with comprehensive data protection and secure backups. It also uses Rsync as a backend and additionally offers the possibility to encrypt backup copies and store them on remote storage media, such as FTP servers, or cloud storage services, such as Amazon S3.

#### Deja Dup

Deja Dup is a graphical backup tool for Ubuntu that simplifies the backup process, allowing us to quickly and easily back up our data. It provides a user-friendly interface to create backup copies of data on local or remote storage media. It uses Rsync as a backend and also supports data encryption.

### Encrypting Backups

In order to ensure the security and integrity of backups, we should take steps to encrypt their backups. Encrypting backups ensures that sensitive data is protected from unauthorized access. Alternatively, we can encrypt backups on Ubuntu systems by utilizing tools such as GnuPG, eCryptfs, and LUKS.

Backing up and restoring data on Ubuntu systems is an essential part of data protection. By utilizing the tools discussed, we can ensure that our data is securely backed up and can be easily restored when needed.

### Install Rsync

To install Rsync on Ubuntu, we can use the `apt` package manager:

```bash
sudo apt install rsync -y
```

This will install the latest version of Rsync on the system. Once the installation is complete, we can begin using the tool to back up and restore data.

### Rsync - Backup a Local Directory to our Backup-Server

To backup an entire directory using Rsync, we can use the following command:

```bash
rsync -av /path/to/mydirectory user@backup_server:/path/to/backup/directory
```

This command will copy the entire directory (`/path/to/mydirectory`) to a remote host (`backup_server`), to the directory `/path/to/backup/directory`. The option `archive` (`-a`) is used to preserve the original file attributes, such as permissions, timestamps, etc., and using the `verbose` (`-v`) option provides a detailed output of the progress of the `rsync` operation.

We can also add additional options to customize the backup process, such as using compression and incremental backups:

```bash
rsync -avz --backup --backup-dir=/path/to/backup/folder --delete /path/to/mydirectory user@backup_server:/path/to/backup/directory
```

With this, we back up the `mydirectory` to the remote `backup_server`, preserving the original file attributes, timestamps, and permissions, and enabled compression (`-z`) for faster transfers. The `--backup` option creates incremental backups in the directory `/path/to/backup/folder`, and the `--delete` option removes files from the remote host that are no longer present in the source directory.

### Rsync - Restore our Backup

If we want to restore our directory from our backup server to our local directory, we can use the following command:

```bash
rsync -av user@remote_host:/path/to/backup/directory /path/to/mydirectory
```

### Encrypted Rsync

To ensure the security of our `rsync` file transfer between our local host and our backup server, we can combine the use of SSH and other security measures. By using SSH, we are able to encrypt our data as it is being transferred, making it much more difficult for any unauthorized individual to access it. Additionally, we can also use firewalls and other security protocols to ensure that our data is kept safe and secure during the transfer. Therefore we tell `rsync` to use SSH like the following:

```bash
rsync -avz -e ssh /path/to/mydirectory user@backup_server:/path/to/backup/directory
```

The data transfer between our local host and the backup server occurs over the encrypted SSH connection, which provides confidentiality and integrity protection for the data being transferred. This encryption process ensures that the data is protected from any potential malicious actors who would otherwise be able to access and modify the data without authorization.

### Auto-Synchronization

To enable auto-synchronization using `rsync`, you can use a combination of `cron` and `rsync` to automate the synchronization process. Scheduling the cron job to run at regular intervals ensures that the contents of the two systems are kept in sync. This can be especially beneficial for organizations that need to keep their data synchronized across multiple machines.

#### RSYNC_Backup.sh

We create a new script called `RSYNC_Backup.sh`, which will trigger the `rsync` command to sync our local directory with the remote one.

```bash
#!/bin/bash

rsync -avz -e ssh /path/to/mydirectory user@backup_server:/path/to/backup/directory
```

Then, in order to ensure that the script is able to execute properly, we must provide the necessary permissions. Additionally, it's also important to make sure that the script is owned by the correct user, as this will ensure that only the correct user has access to the script and that the script is not tampered with by any other user.

```bash
chmod +x RSYNC_Backup.sh
```

After that, we can create a crontab that tells `cron` to run the script every hour at the 0th minute. We can adjust the timing to suit our needs. To do so, the crontab needs the following content:

#### Auto-Sync - Crontab

```bash
0 * * * * /path/to/RSYNC_Backup.sh
```

With this setup, `cron` will be responsible for executing the script at the desired interval, ensuring that the `rsync` command is run and the contents of the local directory are synchronized with the remote host.