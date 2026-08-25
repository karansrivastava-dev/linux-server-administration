# Linux File Permissions & Ownership

This lab demonstrates Linux users, groups, file ownership, directory permissions, file permissions, and group-based access control.

## 1. Create a Practice User

Created a practice user named `devopsks`.

```bash
sudo adduser devopsks
id devopsks
```

## 2. Create a DevOps Group

Created a group named `devops`.

```bash
sudo groupadd devops
getent group devops
```

## 3. Add User to the Group

Added `devopsks` to the `devops` group.

```bash
sudo usermod -aG devops devopsks
groups devopsks
```

## 4. Create a Test Directory and File

Created a directory for the Linux administration lab.

```bash
mkdir ~/linux-admin-lab
touch ~/linux-admin-lab/test.txt
```

## 5. Change File Ownership

Changed the ownership of the test file to the `devopsks` user and `devops` group.

```bash
sudo chown devopsks:devops ~/linux-admin-lab/test.txt
ls -l ~/linux-admin-lab/test.txt
```

## 6. Configure File Permissions

Set the file permission to `640`.

```bash
sudo chmod 640 ~/linux-admin-lab/test.txt
ls -l ~/linux-admin-lab/test.txt
```

The `640` permission means:

- Owner: Read and Write
- Group: Read
- Others: No permissions

## 7. Move Lab to Server Directory

Moved the lab directory to `/srv` to simulate a server-style directory structure.

```bash
sudo mv /home/karansri/linux-admin-lab /srv/linux-admin-lab
sudo chown -R karansri:devops /srv/linux-admin-lab
sudo chmod 750 /srv/linux-admin-lab
sudo chmod 640 /srv/linux-admin-lab/test.txt
```

The `750` directory permission means:

- Owner: Read, Write and Execute
- Group: Read and Execute
- Others: No permissions

## 8. Test Group-Based File Access

Added test content to the file.

```bash
echo "Linux permissions test" > /srv/linux-admin-lab/test.txt
```

Switched to the `devopsks` user.

```bash
su - devopsks
```

Tested file access.

```bash
cat /srv/linux-admin-lab/test.txt
```

Expected output:

```text
Linux permissions test
```

The test confirmed that the `devopsks` user could read the file through membership in the `devops` group.

## 9. Commands Practiced

- `adduser`
- `groupadd`
- `usermod`
- `groups`
- `id`
- `chown`
- `chmod`
- `ls -l`
- `mkdir`
- `touch`
- `mv`
- `cat`
- `su`

## Key Concepts Learned

- Linux user management
- Linux group management
- File ownership
- File permissions
- Directory permissions
- Group-based access control
- Permission troubleshooting
- Server directory structure using `/srv`

## Result

Successfully configured Linux file ownership and group-based access control and verified that a group member could access a file according to the assigned permissions.
