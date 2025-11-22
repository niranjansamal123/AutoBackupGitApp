"AutoBackupGit – Installation Guide

This file explains how to install and run the AutoBackupGit app on Windows.

========================================
1. System Requirements
========================================

- Operating System: Windows 10 or later (64‑bit recommended)
- Git for Windows installed and available in PATH
- .NET Desktop Runtime 8.0 installed

Both Git and .NET 8 MUST be installed for AutoBackupGit to work correctly.

========================================
2. Install .NET Desktop Runtime 8.0
========================================

1) Open a web browser and go to:
   https://dotnet.microsoft.com/en-us/download/dotnet/8.0

2) Under “Run desktop apps”, find:
   “.NET Desktop Runtime 8.x for Windows”

3) Download the installer for your system:
   - Usually “x64” (64‑bit) for modern Windows

4) Run the installer and follow the steps:
   - Accept the license
   - Click Install
   - Wait for completion, then click Close

5) To confirm installation:
   - Optional: open Command Prompt and run:
     `dotnet --list-runtimes`
   - You should see an entry that starts with:
     `Microsoft.WindowsDesktop.App 8.`

========================================
3. Install Git for Windows
========================================

AutoBackupGit calls Git commands internally.  
Without Git, no commits or pushes will happen.

Steps:

1) Open a web browser and go to:
   https://git-scm.com/

2) Click the download link for Windows:
   - “Download for Windows” (this gives you Git for Windows)

3) Run the downloaded installer (e.g., Git‑x.y.z‑64‑bit.exe).

4) When the installer asks for options, you can safely accept defaults:
   - **Select Components**: leave default checked options
   - **Editor**: “Use Vim” or “Use Visual Studio Code” (choose what you like)
   - **PATH environment**:
     - IMPORTANT: Choose  
       “Git from the command line and also from 3rd‑party software”
     - This ensures `git` is available for AutoBackupGit

   - **HTTPS transport backend**:
     - “Use the OpenSSL library” (default)

   - **Line ending conversions**:
     - “Checkout Windows-style, commit Unix-style line endings” (default)

   - **Terminal emulator**, **extra options**, etc.:
     - Keep defaults unless you know what you are changing

5) Click Install and wait until it finishes, then click Finish.

6) Verify Git installation:

   - Open **Command Prompt** (Win+R → type `cmd` → Enter)
   - Run:
     `git --version`

   - You should see output like:
     `git version 2.xx.x.windows.1`

   - If this command fails:
     - Close all Command Prompt windows
     - Log out and log back in, or restart Windows
     - Try again

If `git --version` works, Git is correctly installed and AutoBackupGit can use it.

========================================
4. Files You Receive
========================================

If you downloaded a ZIP:

- AutoBackupGit.exe
- Other .dll and config files in the same folder
- README.md / readme.txt (this file)

If you downloaded a ClickOnce publish folder:

- setup.exe
- AutoBackupGit.application
- Application Files\ (subfolder with versioned files)

Do NOT remove any of the .dll or config files that come with AutoBackupGit.exe.

========================================
5. First-Time Installation (Simple Portable Mode)
========================================

This is the recommended way for most users.

Steps:

1) Create a folder for the app, for example:
   E:\Apps\AutoBackupGit\

2) Extract all contents of the ZIP into this folder.
   After extraction, AutoBackupGit.exe should be inside that folder.

3) (Optional) Create a desktop shortcut:
   - Right-click AutoBackupGit.exe → Send to → Desktop (create shortcut)

4) Double-click AutoBackupGit.exe to run the app.

This is a portable build:
- No installer is required
- No registry entries are created
- To uninstall, just delete the folder and shortcuts

========================================
6. First-Time Installation (ClickOnce setup.exe mode)
========================================

If you received a folder containing setup.exe and AutoBackupGit.application:

1) Open the folder that contains setup.exe.
2) Double-click setup.exe.
3) If Windows shows a SmartScreen or “Unknown publisher” warning:
   - Click “More info”
   - Click “Run anyway”
4) Follow the on-screen prompts.

ClickOnce will:
- Install AutoBackupGit in your user profile
- Add a Start Menu shortcut

To run later:
- Use the Start Menu shortcut
- Or search for “AutoBackupGit” in Windows search

========================================
7. First Launch – Initial Checks
========================================

On first launch, AutoBackupGit will:

1) Create a settings.json file next to the executable.
2) Check Git:
   - If Git is NOT found:
     - A warning message will be shown
     - Install Git (see section 3) and restart the app

3) Check .NET:
   - If the app starts, .NET 8 is already installed
   - If it fails to start, install .NET Desktop Runtime 8.0 (see section 2)

You should see the main window with:
- Start, Stop, History, Settings, Clear Logs, Undo, Changes buttons
- Status text
- Activity log

========================================
8. Configuring Projects (Required Before Backup)
========================================

1) Click the “Settings” button on the main window.
2) In the Projects list, click “+ Add” to add a new project.

For each project, fill:

- Project Name:
  - Any friendly name (e.g., “MyWebsite”, “Portfolio”, “ClientA-App”)

- Project Path:
  - Local folder to monitor and back up
  - Example: D:\Work\MyWebsite

- Remote Repository URL:
  - Your Git repository URL
  - Examples:
    - https://github.com/username/MyWebsite.git
    - git@github.com:username/MyWebsite.git

- Branch:
  - Usually “main” or “master”

- Enable this Project:
  - Check this to activate backup for this project

Per-project options:

- Auto-backup on change:
  - If turned on, backups run soon after files change.

- Enable scheduled backup:
  - If turned on, backups run every X minutes (5, 10, 15, 30, etc.).

3) Click Save.
4) Close the Settings window.

========================================
9. Global Preferences
========================================

In the Settings window (global options):

- Auto-start backup on launch:
  - Start monitoring automatically when AutoBackupGit opens.

- Enable toast notifications:
  - Show Windows notifications when backups succeed or fail.

- Wait before commit (seconds):
  - Delay between detecting file changes and creating the commit
  - Helps group many rapid saves into one commit.

========================================
10. Starting & Stopping Backup
========================================

To start backup:

1) Open AutoBackupGit.
2) Make sure at least one project is enabled and correctly configured.
3) Click “Start Backup”.

The log will show:
- “STARTING MULTI-PROJECT BACKUP SYSTEM”
- Details for each project
- “BACKUP SYSTEM STARTED SUCCESSFULLY”

To stop backup:

- Click “Stop Backup”.
- The log will say “All projects stopped”.

========================================
11. System Tray Behavior
========================================

- When minimized or started, AutoBackupGit may hide to the system tray.
- Look for the AutoBackupGit icon near the clock.
- Double-click the icon to restore the window.
- Right-click for context menu:
  - Open AutoBackupGit
  - Start Backup
  - Stop Backup
  - Exit

========================================
12. History and Restore
========================================

- Click “History” in the main window.
- Choose a project (if multiple).
- Browse commit history.
- Select a commit and click “Restore Selected” to roll back.

Warning:
- This will reset the local repo to that commit and force-push to the remote.
- Use with care: old commits after that point will be removed from the main branch.

========================================
13. Viewing Changes and Partial Commits
========================================

- Click “Changes” to open the change viewer.
- See the list of modified/added/deleted files.
- Preview file diffs.
- Select specific files and commit only those.

========================================
14. Logs and Diagnostics
========================================

- The Activity Log shows all important actions.
- A persistent log file `backup.log` is written next to the EXE.
- Use “Clear Logs” to clear the on-screen view (file remains).

If problems occur:
- Look for “ERROR”, “WARNING”, or “Git error” lines in the log.
- Check:
  - Correct remote URL
  - Internet connectivity
  - Git and .NET installed properly

========================================
15. Updating AutoBackupGit
========================================

Portable:
- Close the app.
- Replace old files with the new version.
- Keep `settings.json` and `backup.log` if you want to preserve settings/history.

ClickOnce:
- If the publisher hosts updates, the app may auto-update.
- Otherwise, run the new setup.exe to install the updated version.

========================================
16. Uninstalling
========================================

Portable:
- Stop backup and close AutoBackupGit.
- Delete the folder where it is stored.
- Optionally delete any shortcuts you created.

ClickOnce:
- Open “Apps & Features” from Windows settings.
- Find “AutoBackupGit” and click Uninstall.

========================================
17. Quick Checklist

Before using AutoBackupGit, make sure:

[ ] .NET Desktop Runtime 8.0 is installed  
[ ] Git for Windows is installed  
[ ] `git --version` works in Command Prompt  
[ ] At least one project is configured in Settings  
[ ] Remote URLs and branch names are correct  
[ ] You have pressed “Start Backup”

If all boxes are checked, AutoBackupGit will automatically monitor and back up your projects using Git, with both automatic and scheduled modes."