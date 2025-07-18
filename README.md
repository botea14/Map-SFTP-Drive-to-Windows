# How to Map SFTP/SSH Servers as Network Drives in Windows
### This tutorial provides a step-by-step guide on how to use SSHFS-Win to connect to SFTP/SSH servers and map their directories as network drives on your Windows computer. This allows you to browse and manage remote files directly from Windows Explorer, just like a local drive.

## Prerequisites: Installation
### Before you can map any drives, you need to install two essential pieces of software.

## Step 1: Install WinFsp
WinFsp (Windows File System Proxy) is a framework that allows you to create user-mode file systems. SSHFS-Win depends on it to function.

+ Download the latest release: WinFsp Releases

+ Download the .msi installer file (e.g., winfsp-2.1.xxxx.msi).

+ Run the installer and follow the on-screen instructions to complete the installation.

## Step 2: Install SSHFS-Win
### SSHFS-Win is the program that provides the SSH File System connectivity.

+ Download the latest release: SSHFS-Win Releases

+ Download the .msi installer file (e.g., sshfs-win-v3.5.xxxx.msi).

+ Run the installer and complete the installation.

## Step 3: Mapping Your Network Drive
### Once the installation is complete, you can map your remote directories. You can do this through the Windows Explorer interface or the Command Prompt.

Option 1: Using Windows Explorer (GUI)
This is the most user-friendly method.

+ Open File Explorer.

+ Right-click on "This PC" in the left-hand navigation pane.

+ Select "Map network drive..." from the context menu.

+ In the "Map Network Drive" window, choose an available Drive letter (e.g., X:, Y:, Z:).

+ In the Folder field, enter the path to your server using the special UNC syntax. See the examples below.

+ Click Finish. You will be prompted to enter the username and password for the remote server.

Windows Explorer Examples:
Example A: Mapping the server's root directory (/)

To map the entire file system of a server, use the sshfs.r prefix.

Server: linux.intra

Username: your_user

Path: \\sshfs.r\your_user@linux.intra

Example B: Mapping a specific folder (e.g., /mnt/storage)

To map a specific folder deep in the file system, also use the sshfs.r prefix and add the path at the end.

Server: game.inewb.ro

Username: root

Path: \\sshfs.r\root@game.inewb.ro\mnt\storage

Example C: Mapping a user's home directory (~)

To map only the home directory of the remote user, use the sshfs prefix (without the .r).

Server: game.inewb.ro

Username: root

Path: \\sshfs\root@game.inewb.ro

Option 2: Using the Command Line (net use)
This method is faster for users comfortable with the command line.

Open Command Prompt or PowerShell.

Use the net use command followed by a drive letter and the server path.

You will be prompted to enter the password for the remote user.

Command Line Examples:
Example A: Mapping the server's root directory (/)

net use Z: \\sshfs.r\your_user@linux.intra

Example B: Mapping a specific folder (e.g., /home)

net use Y: \\sshfs.r\root@game.inewb.ro\home

Example C: Mapping another specific folder (e.g., /mnt/storage)

net use X: \\sshfs.r\root@game.inewb.ro\mnt\storage

How to Unmap a Drive
To disconnect a drive, you can either:

GUI: Right-click the network drive in "This PC" and select "Disconnect".

Command Line: Use the net use command with the /delete switch.

net use Z: /delete
