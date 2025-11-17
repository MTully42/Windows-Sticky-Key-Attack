Sticky Keys Attack: A Comprehensive Guide

Introduction

The Sticky Keys attack is a classic example of a privilege escalation vulnerability that exploits a legitimate Windows accessibility feature.^1^ While often considered an older attack vector, it still serves as an excellent educational tool for understanding system vulnerabilities, defense mechanisms, and the importance of proper system configuration. This guide will provide a detailed explanation of the Sticky Keys attack, its mechanics, how to perform it, and crucially, how to defend against it.

What are Sticky Keys?

Sticky Keys is an accessibility feature in Microsoft Windows designed to help users who have difficulty holding down multiple keys simultaneously.^2^ When Sticky Keys is enabled, pressing a modifier key (like Shift, Ctrl, Alt, or the Windows key) once will \"stick\" it, allowing the user to press other keys sequentially as if the modifier key were still being held down.^3^ Pressing the modifier key again will \"unstick\" it. This feature is typically activated by pressing the Shift key five times in quick succession.^4^

The Vulnerability

The vulnerability lies in the fact that the executable responsible for the Sticky Keys feature (sethc.exe) can be swapped with another executable, such as cmd.exe (the command prompt).^5^ When sethc.exe is launched from the Windows logon screen (by pressing Shift five times), the swapped cmd.exe will be launched instead, but with the SYSTEM privileges of the logon screen. This provides an attacker with a highly privileged command prompt before even logging into the system.

How the Attack Works

The Sticky Keys attack typically involves the following steps:

1.  **Access to the Target System (Physical or Remote with Specific Privileges):** The attacker needs a way to modify files on the target system\'s hard drive. This could be physical access (booting from a USB drive or removing the hard drive), or remote access if they have sufficient privileges to write to system directories.^6^

2.  **Renaming sethc.exe:** The original sethc.exe file is located in C:\Windows\System32. ^7^The attacker renames it to something like sethc.bak to preserve it.

> ![Hacker renaming sethc.exe](media/image1.png){width="5.333333333333333in" height="5.333333333333333in"}

3.  **Copying cmd.exe:** The attacker then copies cmd.exe (also located in C:\Windows\System32) and renames the copy to sethc.exe.^8^

> ![Copy & Rename](media/image2.png){width="5.333333333333333in" height="5.333333333333333in"}

4.  **Triggering the Attack:** The attacker reboots the system (or waits for it to be at the logon screen). At the logon screen, they press the Shift key five times.^9^

> ![5 Shift Key Hits & Boom](media/image3.png){width="5.333333333333333in" height="5.333333333333333in"}

5.  **Gaining a SYSTEM Shell:** Instead of the Sticky Keys prompt, a command prompt window appears with SYSTEM privileges.

> ![Full Privilege Escalation](media/image4.png){width="5.333333333333333in" height="5.333333333333333in"}
