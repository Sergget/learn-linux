# Onedrive 使用

## 安装

> sudo apt install onedrive

## 基本使用
       onedrive - [文件] 与onedrive进行同步

## 概要
- onedrive [OPTION] --synchronize
- onedrive [OPTION] --monitor
- onedrive [OPTION] --display-config
- onedrive [OPTION] --display-sync-status

## 描述
A complete tool to interact with OneDrive on Linux.

## 选项
Without any option given, no sync is done and the program exits.

-  --check-for-nomount
        Check  for  the  presence  of .nosync in the syncdir root. If found, do not perform
        sync.

-  --confdir ARG
        Set the directory used to store the configuration files

-  --create-directory ARG
        Create a directory on OneDrive - no sync will be performed.

-  --destination-directory ARG
        Destination directory for renamed or move on OneDrive - no sync will be performed.

-  --debug-https
        Debug OneDrive HTTPS communication.

-  --disable-notifications
        Do not use desktop notifications in monitor mode

-  --disable-upload-validation
        Disable upload validation when uploading to OneDrive

-  --display-config
        Display what options the client will use as currently configured - no sync will  be
        performed.

-  --display-sync-status
        Display the sync status of the client - no sync will be performed.

- -d --download-only
        Only download remote changes

-  --enable-logging
        Enable client activity to a separate log file

-  --force-http-1.1
        Force the use of HTTP 1.1 for all operations

-  --get-O365-drive-id ARG
        Query  and  return the Office 365 Drive ID for a given Office 365 SharePoint Shared
        Library

-  --local-first
        Synchronize from the local directory source first, before downloading changes  from
        OneDrive.

-  --logout
        Logout the current user

- -m --monitor
        Keep monitoring for local and remote changes

-  --no-remote-delete
        Do not delete local file 'deletes' from OneDrive when using-  --upload-only

-  --print-token
        Print the access token, useful for debugging

-  --resync
        Forget the last saved state, perform a full sync

-  --remove-directory ARG
        Remove a directory on OneDrive - no sync will be performed.

-  --single-directory ARG
        Specify a single local directory within the OneDrive root to sync.

-  --skip-symlinks
        Skip syncing of symlinks

-  --source-directory ARG
        Source directory to rename or move on OneDrive - no sync will be performed.

-  --syncdir ARG
        Set the directory used to sync the files that are synced

-  --synchronize
        Perform a synchronization

-  --upload-only
        Only upload to OneDrive, do not sync changes from OneDrive locally

- -v --verbose
        Print  more  details,  useful for debugging. Given two times (or more) enables even
        more verbose debug statements.

-  --version
        Print the version and exit

- -h --help
        This help information.

## 特性
       State caching

       Real-Time file monitoring with Inotify

       Resumable uploads

       Support OneDrive for Business (part of Office 365)

       Shared folders (OneDrive Personal)

       SharePoint / Office 365 Group Drives (refer to README.Office365.md to configure)

## 配置文件
 You should copy the default config file into your home directory before making changes:
 mkdir -p ~/.config/onedrive
 cp /usr/share/doc/onedrive/config ~/.config/onedrive/config

 Available options:

- sync_dir
        directory where the files will be synced

- skip_file
        any files that match this pattern will be skipped during sync

- skip_symlinks
        skip symbolic links during sync, defaults to "false"

- monitor_interval
        the number of seconds by which each sync operation is undertaken  when  idle  under
        monitor mode, defaults to "45"

- log_dir
        defines the directory where logging output is saved to, needs to end with a slash

 Pattern  are  case  insensitive.   *  and  ? wildcards characters are supported.  Use | to
 separate multiple patterns.

 After changing the filters (skip_file or  skip_dir  in  your  configs)  you  must  execute
 >onedrive --synchronize --resync.

## 首次运行
After  installing  the  application  you  must  run  it at least once from the terminal to
authorize it.

You will be asked to open a specific link using your web browser where you  will  have  to
login  into  your Microsoft Account and give the application the permission to access your
files. After giving the permission, you will be redirected to a blank page. Copy  the  URI
of the blank page into the application.

## 与SYSTEMD 整合
Service files are installed into user and system directories.

OneDrive service running as root user
      To enable this mode, run as root user
> systemctl enable onedrive
>
> systemctl start onedrive

### OneDrive service running as root user for a non-root user
This  mode allows starting the OneDrive service automatically with system start for multiple users. For each `<username>` run:
>systemctl enable onedrive@`<username>`
>
>systemctl start onedrive@`<username>`

### OneDrive service running as non-root user

In this mode the service will be started when the user logs in.  Run as user
- systemctl --user enable onedrive
- systemctl --user start onedrive

## LOGGING OUTPUT
       When running onedrive all actions can be logged to a  separate  log  file.   This  can  be
       enabled  by  using  the  --enable-logging  flag.  By default, log files will be written to
       /var/log/onedrive.

       All logfiles will be in the format of %username%.onedrive.log, where %username% represents
       the user who ran the client.

## NOTIFICATIONS
       If  OneDrive  has  been  compiled  with  support  for notifications, a running onedrive in
       monitor mode will send notifications about initialization and errors via libnotify to  the
       dbus.

       Note  that  this  does  not  work  if  onedrive  is  started  as  root  for a user via the
       onedrive@<username> service.

## SEE ALSO
       Further examples  and  documentation  is  available  in  /usr/share/doc/onedrive/README.md
       /usr/share/doc/onedrive/README.Office365.md