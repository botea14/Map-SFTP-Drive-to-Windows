# How to Map SFTP/SSH Servers as Network Drives in Windows 🗺️

This tutorial provides a step-by-step guide on how to use **SSHFS-Win** to connect to SFTP/SSH servers and map their directories as network drives on your Windows computer. This allows you to browse and manage remote files directly from **Windows Explorer**, just like a local drive.

---

## 💾 Prerequisites: Installation
Before you can map any drives, you need to install two essential pieces of software.

### Step 1: Install WinFsp
> [!NOTE]
> **WinFsp** (Windows File System Proxy) is a framework that allows you to create user-mode file systems. SSHFS-Win depends on it to function.

* **Download the latest release:** [**WinFsp Releases**](https://github.com/winfsp/winfsp/releases)
* Download the `.msi` installer file (e.g., `winfsp-2.1.xxxx.msi`).
* Run the installer and follow the on-screen instructions to complete the installation.

### Step 2: Install SSHFS-Win
> [!NOTE]
> **SSHFS-Win** is the program that provides the SSH File System connectivity.

* **Download the latest release:** [**SSHFS-Win Releases**](https://github.com/winfsp/sshfs-win/releases)
* Download the `.msi` installer file (e.g., `sshfs-win-v3.5.xxxx.msi`).
* Run the installer and complete the installation.

---

## 🔗 Step 3: Mapping Your Network Drive
Once the installation is complete, you can map your remote directories. You can do this through the Windows Explorer interface or the Command Prompt.

### Option 1: Using Windows Explorer (GUI)
This is the most user-friendly method.

1. Open **File Explorer**.
2. Right-click on **"This PC"** in the left-hand navigation pane.
3. Select **"Map network drive..."** from the context menu.
4. In the "Map Network Drive" window, choose an available **Drive letter** (e.g., `X:`, `Y:`, `Z:`).
5. In the `Folder` field, enter the path to your server using the special UNC syntax. See the examples below.
6. Click **Finish**. You will be prompted to enter the username and password for the remote server.

#### **Windows Explorer Examples**

| **Goal** | **Server** | **Username** | **Path to Enter** |
| :--- | :--- | :--- | :--- |
| **Map Root (`/`)** | `linux.intra` | `root` | `\\sshfs.r\root@linux.intra` |
| **Map Specific Folder** | `linux.intra` | `root` | `\\sshfs.r\root@linux.intra\mnt\storage` |
| **Map Home Dir (`~`)** | `linux.intra` | `root` | `\\sshfs\root@linux.intra` |

> [!TIP]
> * Use `\\sshfs.r\` to start from the server's **root** directory (`/`).
> * Use `\\sshfs\` to start from the user's **home** directory (`~`).

### Option 2: Using the Command Line (`net use`)
This method is faster for users comfortable with the command line.

1. Open **Command Prompt** or **PowerShell**.
2. Use the `net use` command followed by a drive letter and the server path.
3. You will be prompted to enter the password for the remote user.

#### **Command Line Examples**

**Example A: Mapping the server's root directory (`/`)**
```cmd
net use Z: \\sshfs.r\root@linux.intra
```

**Example B: Mapping a specific folder (e.g., `/home`)**
```cmd
net use Y: \\sshfs.r\root@linux.intra\home
```

**Example C: Mapping another specific folder (e.g., `/mnt/storage`)**
```cmd
net use X: \\sshfs.r\root@linux.intra\mnt\storage
```

---

## 🗑️ How to Unmap a Drive
To disconnect a drive, you can either:

* **GUI:** Right-click the network drive in **"This PC"** and select **"Disconnect"**.

* **Command Line:** Use the `net use` command with the `/delete` switch.
    > [!WARNING]
    > This action is immediate and will disconnect the drive.

    ```cmd
    net use Z: /delete
    
