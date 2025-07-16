# Section 5

## Enhance!
tag: `Medium`, `Forensics`, `picoCTF 2022`, `svg`

### Description
Download this image file and find the flag.
- **Download image file**

### Solving Steps 
1. Click **Download image file** download the drawing.flag.svg
2. Open drawing.flag.svg in the browser.
3. Right click the mouse and press "copy"
4. You will get the flag:
    ```
    picoCTF{3nh4nc3d_aab729dd}
    ```

### Flag
    picoCTF{3nh4nc3d_aab729dd}

### Notes
- SVG is a vector image format based on XML, where text elements are actual text nodes rather than just pixels like in raster images.  
- Because SVG files can be viewed and copied directly in browsers or text editors, many CTF challenges use SVG to hide flags.  
- Opening the SVG in a browser and copying the text directly is the quickest and simplest way to extract hidden information, without needing extra tools or decoding.  
- When handling similar files, besides using browsers, text editors or XML parsing tools can also be used to quickly locate hidden content.
---

## Big Zip
tag: `Easy`, `General Skills`, `picoGym Exclusive`

### Description
Unzip this archive and find the flag.
**Download zip file**

### Hints
- Can grep be instructed to look at every file in a directory and its subdirectories?

### Solving Steps 
1. Click **Download zip file** download big-zip-files.zip
2. Open linux terminal to unzip the file
    ```
    unzip big-zip-files.zip
    ```
3. Use `grep -R "string_to_be_searched" "directory_path"` to search the flag at every file in a directory and its subdirectories.
    ```
    grep -R picoCTF big-zip-files
    ```
4. The flag will be displayed:
    ```
    big-zip-files/folder_pmbymkjcya/folder_cawigcwvgv/folder_ltdayfmktr/folder_fnpfclfyee/whzxrpivpqld.txt:information on the record will last a billion years. Genes and brains and books encode picoCTF{gr3p_15_m4g1c_ef8790dc}
    ```

### Flag
    picoCTF{gr3p_15_m4g1c_ef8790dc}

### Notes
- The `-R` option in `grep` allows searching through all files in a directory and its subdirectories, making it useful for large, nested archives.  
- Unzipping large archives with many nested folders can be time-consuming; using recursive grep saves time by automating the search for specific strings.  
---

## vault-door-training
tag: `Easy`, `Reverse Engineering`, `picoCTF 2019`

### Description
Your mission is to enter Dr. Evil's laboratory and retrieve the blueprints for his Doomsday Project. The laboratory is protected by a series of locked vault doors. Each door is controlled by a computer and requires a password to open. Unfortunately, our undercover agents have not been able to obtain the secret passwords for the vault doors, but one of our junior agents obtained the source code for each vault's computer! You will need to read the source code for each level to figure out what the password is for that vault door. As a warmup, we have created a replica vault in our training facility. The source code for the training vault is here: **VaultDoorTraining.java**

### Hints
- The password is revealed in the program's source code.

### Solving Steps 
1. Click **VaultDoorTraining.java** download VaultDoorTraining.java
2. Open linux terminal, use `cat` command to fetch the text in the file.
    ```
    cat VaultDoorTraining.java
    ```
3. The flag will be displayed:
    ```java
    // The password is below. Is it safe to put the password in the source code?
    // What if somebody stole our source code? Then they would know what our
    // password is. Hmm... I will think of some ways to improve the security
    // on the other doors.
    //
    // -Minion #9567
    public boolean checkPassword(String password) {
        return password.equals("w4rm1ng_Up_w1tH_jAv4_be8d9806f18");
    ```

### Flag 
    picoCTF{w4rm1ng_Up_w1tH_jAv4_be8d9806f18}

### Notes
- In this challenge, the flag is directly embedded in the source code, demonstrating poor security practices like hardcoding passwords.  
- Java source files (`.java`) are plain text and can be easily inspected using tools like `cat` or any text editor.  
- This challenge reinforces the importance of **never storing sensitive credentials directly in code**, especially in production environments.  
---

## keygenme-py
tag: `Medium`, `Reverse Engineering`, `picoCTF 2021`

### Description
**keygenme.py**

### Solving Steps 
1. Click **keygenme.py** to download keygenme.py.
2. Open the file and observe the logic inside the `check_key` function. It uses a `username_trial` (`"GOUGH"`) and calculates a SHA-256 hash of it using its byte version (`b"GOUGH"`) to verify if the user-provided license key is correct.
3. The license key structure is as follows:
    ```
    picoCTF{1n_7h3_|<3y_of_XXXXXXXX}
    ```
    where the dynamic part is constructed from specific characters of the SHA-256 hash of `b"GOUGH"`:
    - hash[4], hash[5], hash[3], hash[6], hash[2], hash[7], hash[1], hash[8]
4. Write a small Python script to calculate the dynamic part of the license key:
    ```python
    import hashlib

    username_trial = "GOUGH"
    bUsername_trial = b"GOUGH"

    key_part_static1_trial = "picoCTF{1n_7h3_|<3y_of_"
    key_part_dynamic1_trial = ""
    key_part_static2_trial = "}"

    hash = hashlib.sha256(bUsername_trial).hexdigest()

    #build string
    key_part_dynamic1_trial += hash[4]
    key_part_dynamic1_trial += hash[5]
    key_part_dynamic1_trial += hash[3]
    key_part_dynamic1_trial += hash[6]
    key_part_dynamic1_trial += hash[2]
    key_part_dynamic1_trial += hash[7]
    key_part_dynamic1_trial += hash[1]
    key_part_dynamic1_trial += hash[8]

    key_full_template_trial = key_part_static1_trial + key_part_dynamic1_trial + key_part_static2_trial

    print(key_full_template_trial)
    ```
5. Run the script. The result will be:
    ```
    picoCTF{1n_7h3_|<3y_of_f911a486}
    ```
6. Launch the program:
    ```bash
    python3 keygenme-trial.py
    ```
7. Choose option `c` and input the license key:
    ```
    picoCTF{1n_7h3_|<3y_of_f911a486}
    ```
8. If the key is correct, the program will write a new file called `keygenme.py`.

### Flag  
    picoCTF{1n_7h3_|<3y_of_f911a486}

### Notes  
- The license key is dynamically generated based on the SHA-256 hash of the username `"GOUGH"`.
- The static and dynamic parts are combined to form the final license key.
---


## buffer overflow 0
tag: `Medium`, `Binary Exploitation`, `picoCTF 2022`, `gets`

### Description
Let's start off simple, can you overflow the correct buffer? The program is available **here**. You can view source **here**.

### Hints
- How can you trigger the flag to print?
- If you try to do the math by hand, maybe try and add a few more characters. Sometimes there are things you aren't expecting.
- Run `man gets` and read the BUGS section. How many characters can the program really read?

### Solving Steps 
1. Click **here** to download vuln and vuln.c files.
2. Click **Start Instance**, the description will update to:
    ```
    Let's start off simple, can you overflow the correct buffer? The program is available here. You can view source here.
    Connect using:
    nc saturn.picoctf.net 59468
    ```
3. Open the source file and observe the following function:
    ```c
    void vuln(char *input){
        char buf2[16];
        strcpy(buf2, input);
    }
    ```
    This function copies user input into a 16-byte buffer using strcpy, a function that does not check bounds. If the input exceeds 16 bytes, a buffer overflow occurs.

    In the main() function, there is a signal handler configured:
    ```c
    signal(SIGSEGV, sigsegv_handler);
    ```
    This means if a segmentation fault happens (commonly caused by buffer overflow), the sigsegv_handler function will be called:
    ```c
    void sigsegv_handler(int sig) {
        printf("%s\n", flag);
        exit(1);
    }
    ```
    The flag is read from flag.txt and printed when the handler is triggered.
4. Use `nc` to connect to the remote service:
    ```bash
    nc saturn.picoctf.net 58056
    ```
5. When prompted:
    ```bash
    Input: 
    ```
    Enter a long string to overflow the buffer:
    `AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA`
6. The program crashes and prints the flag due to the signal handler:
    ```
    picoCTF{ov3rfl0ws_ar3nt_that_bad_ef01832d}
    ```

### Flag 
    picoCTF{ov3rfl0ws_ar3nt_that_bad_ef01832d}\

### Notes
- Instead of avoiding a crash, your goal is to cause a crash (segfault), which triggers a custom signal handler that reveals the flag.
- The program is designed to help you learn that unsafe C functions like `strcpy()` (or `gets()`) can allow overflows if input isn’t validated.
---

