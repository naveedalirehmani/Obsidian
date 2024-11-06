
drwxr-xr-x 2 root root 4096 Sep 12 11:36 folderName

`drwxr-xr-x`

1. Let's break this down. `d` here stands for a directory a simple `-` here would mean that this is a file.
2. `rwx r-x r-x` this represents the read, write and execute permissions for owner, group and others users respectively. A simple `-` means that this respective users has no permission for this action.
3. to change the owner or group of a file you can use chown which means change-owner to change the owner and group of the file above you can write `chown ubuntu:<second-user-name> <filename>`
4. Each of these permission are represented by a number such as for `read`, `write` & `execute` we have `4`, `2` & `1` 
5. So to change permission for each user you can type `chmod` here `chmod` stands for change-mode `chmod 774 filename` which will change the permissions to `drwxrwxr--` 

