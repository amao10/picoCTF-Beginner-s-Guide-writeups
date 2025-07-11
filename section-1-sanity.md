# Section 1 (Sanity)

## Obedient Cat
tag: Easy, General Skills, picoCTF 2021

### Description
This file has a flag in plain sight (aka "in-the-clear")

### Solving Steps
1. Press **Download flag**.
2. Open a linux terminal.
3. Navigate to the directory where the file is located using the `cd` command.
4. Use the `cat` command to display the file content:

    ```bash
    cat flag
    ```
5. The terminal will print the flag in plain text:

    ```
    picoCTF{s4n1ty_v3r1f13d_2fd6ed29}
    ``` 
### Notes
- The challenge name **Obedient Cat** is a hint to use the `cat` command.
- **In-the-clear** means the flag is unencrypted and directly viewable.
---

## Super SSH
tag: Easy, General Skills, picoCTF 2024, shell, ssh, browser_webshell_solvable

### Description
Using a Secure Shell (SSH) is going to be pretty important.
Additional details will be available after launching your challenge instance.

### Solving Steps
1. Press **Launch Instance**, the current status changed from **NOT RUNNING** to **RUNNING**. The descrption updates to:
    ```
    Using a Secure Shell (SSH) is going to be pretty important.
    Can you ssh as ctf-player to titan.picoctf.net at port 50777 to get the flag?
    You'll also need the password 6abf4a82. If asked, accept the fingerprint with yes.
    If your device doesn't have a shell, you can use: https://webshell.picoctf.org
    If you're not sure what a shell is, check out our Primer: https://primer.picoctf.com/#_the_shell
    ```

2. Open a terminal.
3. Use the following SSH command to connect:
    ```bash 
    ssh ctf-player@titan.picoctf.net -p 50777
    ```
4. When prompted with:
    ```
    Are you sure you want to continue connecting (yes/no/[fingerprint])?```
Enter:`yes`
5. When ask for the password:
    ```
    ctf-player@titan.picoctf.net's password:
    ```
Enter:`6abf4a82`
6. The terminal will print the flag:
    ```
    Welcome ctf-player, here's your flag: picoCTF{s3cur3_c0nn3ct10n_65a7a106}
    Connection to titan.picoctf.net closed.
    ```

### Flag
    ```
    picoCTF{s3cur3_c0nn3ct10n_65a7a106}
    ```

### Notes
- This challenge introduces basic usage of SSH to connect to remote machines.
- If you're unfamiliar with SSH or terminal environments, the picoCTF webshell is a great alternative: https://webshell.picoctf.org
- Accepting the fingerprint is standard when connecting to a host for the first time.
---

## What's a net cat?
tag: Easy, General Skills, picoCTF 2019

### Description
Using netcat (nc) is going to be pretty important. Can you connect to jupiter.challenges.picoctf.org at port 25103 to get the flag?

### Solving Steps
1. Open linux terminal.
2. Use the `nc` (netcat) command to connect to the target server and port:
    ```bash
    nc jupiter.challenges.picoctf.org 25103
    ```
3. The server will return the flag immediately:
    ```
    You're on your way to becoming the net cat master
    picoCTF{nEtCat_Mast3ry_d0c64587}
    ```

### Flag
    ```
    picoCTF{nEtCat_Mast3ry_d0c64587}
    ```

### Notes  
- `nc` (netcat) is a command-line utility used to read and write data across network connections using TCP or UDP.
- The syntax `nc <host> <port>` connects directly to a remote service.
- This challenge requires no user input — connecting is enough to receive the flag.
- If `nc` is not installed, use the following command to install it (Debian/Ubuntu):
    ```bash
    sudo apt install netcat
    ```
---
