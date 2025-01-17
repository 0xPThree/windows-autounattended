# Unattended Windows Installation

## Overview

Microsoft allows you to add Answer Files (or Unattend files) to Windows ISO files, which can be used to modify Windows settings in the Windows Image (ISO) during the Windows Setup process.

More info on Answer files can be found here: [Microsoft Docs on Answer Files](https://learn.microsoft.com/en-us/windows-hardware/manufacture/desktop/update-windows-settings-and-scripts-create-your-own-answer-file-sxs?view=windows-11) 

The attached answer file(s) automates many parts of the Windows setup and will save you a ton of time when doing a fresh install of Windows, it's debloated and customized to more or less only have PowerShell, Command Prompt, Notepad and Calculator installed.

The answer file works on both Windows 10 and Windows 11, and I’ve tested it on the Pro version of Windows 10 22H2 and Windows 11 23H2 without any issues. A fresh Windows 11 install will run with only about 70 (!) active processes.

![69-processes.img](https://github.com/0xPThree/windows-autounattended/assets/108757172/32797f8c-02f2-48e6-803c-c99bfd917233)

## Why should I use an answer file?

In my opinion, the best thing about an answer file is that it’s very safe.

1. You can see every single change it will make to the Windows Image by inspecting the answer file.
2. You insert it on the Official Windows 10 or 11 ISO directly from Microsoft, no need to download ISO files from Unofficial sources.
3. It's not dependent on any third party tools and is an Official Microsoft Feature used to make Mass Windows Deployments easier.

## What does this answer file do?

Almost all of the tweaks in the [autounattended.xml](https://github.com/0xPThree/windows-autounattended/blob/main/autounattend.xml) answer file have descriptions, and you can inspect it right here on GitHub.

Alternatively, you can download the file and use any text editor of your choise to open it, inspect it and make changes to it if needed.  
  
### But in short it does the following

- **Bypasses Windows 11 System Requirements**:
  - Adds registry entries to bypass TPM, Secure Boot, Storage, CPU, RAM, and Disk checks.

- **Debloats Windows**:
  - Removes preinstalled bloatware apps using PowerShell scripts.
  - Removes legacy apps using PowerShell scripts.

- **Registry Tweaks**:
  - Disables Microsoft Account creation.
  - Disables User Account Control (UAC).
  - Disables lock screen and Windows Spotlight.
  - Customizes Start Menu and Taskbar settings.
  - Disables various Windows features like Cortana, Telemetry, Hibernation, and Location Tracking.
  - Configures Windows Update to only install security updates and delay other updates for 2 years.
  - Disables Windows Error Reporting, Delivery Optimization, and Remote Assistance.
  - Sets various performance and privacy-related registry keys.

- **Runs Custom Scripts**:
  - Executes PowerShell and batch scripts to apply additional tweaks and remove specific applications like Microsoft Edge, OneDrive, and Teams.
  - Loads and unloads the Default User registry hive to apply settings for new users.

- **Service Configurations**:
  - Sets numerous Windows services to manual or disabled to optimize performance.

- **Power Plan**:
  - Enables and sets the Ultimate Performance power plan as active.

- **Miscellaneous**:
  - Creates a desktop shortcut for Chris Titus Windows Utility.
  - Disables IPv6 and Teredo.
  - Disables various scheduled tasks related to telemetry and diagnostics.
  - Enables Dark Mode by default.
  - Aligns the Start Button in Windows 11 to the left by default.

It also contains elements and scripts from the following sources:

- Base Answer File generation:
  - [Schneegans Unattend Generator](https://schneegans.de/windows/unattend-generator/)
- Windows Tweaks & Optimizations:
  - [ChrisTitusTech WinUtil](https://github.com/ChrisTitusTech/winutil)
- Various Tweaks:
  - [Tiny11Builder](https://github.com/ntdevlabs/tiny11builder)
  - [Ten Forums](https://www.tenforums.com/)
  - [Eleven Forum](https://www.elevenforum.com/)
  - [Winaero Tweaker](https://winaerotweaker.com/)

> [!NOTE]
> Due to the removal of Microsoft Edge, I've include a Powershell Script on the Desktop called "LAUNCH-CTT-WINUTIL.ps1"

- Make sure you are connected to the internet, then right click on this file and select Run with Powershell.
- It will launch the Chris Titus Tech Windows Utility and you can use that to install your browser of choice (even Edge) and any other software for that matter.

![LAUNCH-CTT-WINUTIL.ps1](https://github.com/0xPThree/windows-autounattended/assets/108757172/35b80f5d-f327-44cc-b96b-5c3207c0ea29)


## Usage Instructions

In short, you need to include the [autounattended.xml](https://github.com/0xPThree/windows-autounattended/blob/main/autounattend.xml) answer file on your Windows Installation Media so it can be read and executed during the Windows Setup. Here are a few ways to do it:

### Method 1: Create a Bootable Windows Installation Media

1. Download the [autounattended.xml](https://github.com/0xPThree/windows-autounattended/blob/main/autounattend.xml) file and save it on your computer.
2. Create a Windows 10 or 11 Bootable Installation USB drive with the Media Creation Tool or Rufus, for example. (When using Rufus, don’t select any of the checkboxes in “Customize Your Windows Experience” as it creates another answer file, we don't want that.)
   - [Download Windows 10](https://www.microsoft.com/en-us/software-download/windows10)
   - [Download Windows 11](https://www.microsoft.com/en-us/software-download/windows11)
   - [Rufus](https://rufus.ie/en/)
3. Copy the autounattended.xml file you downloaded in Step 1 to the root of the Bootable Windows Installation USB you created in Step 2.
4. Boot from the Windows Installation USB, do a clean install of Windows as normal, and the scripts will run automatically.

### Method 2: Create a Custom ISO File

1. Download the [autounattended.xml](https://github.com/0xPThree/windows-autounattended/blob/main/autounattend.xml) file and save it on your computer.
2. Download the Windows 10 or Windows 11 ISO file depending on the version you want.
   - [Download Windows 10](https://www.microsoft.com/en-us/software-download/windows10)
   - [Download Windows 11](https://www.microsoft.com/en-us/software-download/windows11)
3. Download and Install AnyBurn: [AnyBurn](https://anyburn.com/download.php)
   - In AnyBurn, select the “Edit Image File” option.
   - Navigate to and select the Official Windows ISO file you downloaded in Step 2.
   - Click on “Add” and select the autounattended.xml file you downloaded in Step 1 or just click and drag the autounattended.xml into the AnyBurn window.
   - Click on “Next,” then on “Create Now.” You should be prompted to overwrite the ISO file, click on “Yes.”
   - Once the process is complete, close AnyBurn.
4. Use this ISO file to Install Windows on a Virtual Machine OR use a program like Rufus or Ventoy to create a bootable USB flash drive with the edited Windows ISO file. (When using Rufus, don’t select any of the checkboxes in “Customize Your Windows Experience” as it creates another answer file, we don't want that.)
   - [Rufus](https://rufus.ie/en/)
   - [Ventoy](https://www.ventoy.net/)
5. Boot from the Windows Installation USB, do a clean install of Windows as normal, and the scripts will run automatically.

## Known-Issues

1. If you want to install and use Adobe Creative Cloud then you need to reinstall Microsoft Edge or else the Adobe Installer won't run.
   - Open Windows Powershell as admin and run the following command to reinstall Microsoft Edge (or use the Chris Titus Windows Utility)
     
     ```
     winget install -e --id Microsoft.Edge
     ```
  
