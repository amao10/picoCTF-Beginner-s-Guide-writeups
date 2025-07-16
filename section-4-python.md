# Section 4 (Python)

## Python Wrangling
tag: `Easy`, `General Skills`, `picoCTF 2021`

### Description
Python scripts are invoked kind of like programs in the Terminal... Can you run **this Python script** using **this password** to get **the flag**?

**Hints**:
- Get the Python script accessible in your shell by entering the following command in the Terminal prompt: $ wget https://mercury.picoctf.net/static/5c4c0cbfbc149f3b0fc55c26f36ee707/ende.py
- `$ man python`

### Solving Steps 
1. Click **this Python script**, **this password**, and **the flag** to download the three files:
    - ende.py(Python script)
    - pw.txt(password)
    - flag.txt.en(flag).
2. Open a terminal.
3. Use the cat command to view the contents of the password file:
    ```bash
    cat pw.txt
    ```
    Output:
    ```
    192ee2db192ee2db192ee2db192ee2db
    ```
4. Use the Python script to decrypt the flag:
    ```
    python3 ende.py -d flag.txt.en
    ```
5. When prompted:
    ```
    Please enter the password:
    ```
    Enter the password:
    ```
    192ee2db192ee2db192ee2db192ee2db
    ```
7. The flag will be displayed:
    ```
    picoCTF{4p0110_1n_7h3_h0us3_192ee2db}
    ```

### Flag
    picoCTF{4p0110_1n_7h3_h0us3_192ee2db}

### Notes 
- Python scripts can behave like traditional CLI tools when invoked with flags and arguments.
- Always read the script or run it without arguments to reveal usage instructions.
- You can inspect the script’s logic using:

```bash
cat ende.py
```
- The -d flag in this challenge indicates "decrypt," while -e (not used here) would be "encrypt."
---

## PW Crack 1
tag: `Easy`, `General Skills`, `Beginner picoMini 2022`, `password_cracking`

### Description
Can you crack the password to get the flag?
Download the password checker **here** and you'll need the encrypted **flag** in the same directory too.

**Hints**:
- To view the file in the webshell, do: $ nano level1.py
- To exit nano, press Ctrl and x and follow the on-screen prompts.
- The str_xor function does not need to be reverse engineered for this challenge.

### Solving Steps 
1. View the source code of the password checker script:
    ``` 
    cat level1.py
    ```
2. Inspecting the source code reveals the password is hardcoded in the function:
    ```
    def level_1_pw_check():
    user_pw = input("Please enter correct password for flag: ")
    if( user_pw == "691d"):
        print("Welcome back... your flag, user:")
        decryption = str_xor(flag_enc.decode(), user_pw)
        print(decryption)
        return
    print("That password is incorrect")
    ```
    > The passward is :691d
3. Run the password checker script:
    ```
    python3 level1.py
    ```
4. When prompt:
    ```
    Please enter correct password for flag: 
    ```
    Enter: `691d`
5. The flag will be displayed:
    ```
    Welcome back... your flag, user:
    picoCTF{545h_r1ng1ng_56891419}
    ```
### Flag
    picoCTF{545h_r1ng1ng_56891419}

### Notes
- This challenge demonstrates a basic form of static analysis—reading and understanding a Python script to extract hardcoded values.
- The password is not dynamically generated; it is directly written in the source code, making it easy to retrieve by inspecting the script.
- The str_xor() function handles the decryption using the password, but its internal logic is not required for solving the challenge.
---

## PW Crack 2
tag: `Easy`, `General Skills`, `Beginner picoMini 2022`, `password_cracking`

### Description
Can you crack the password to get the flag?
Download the password checker **here** and you'll need the encrypted **flag** in the same directory too.

**Hints**:
- Does that encoding look familiar?
- The str_xor function does not need to be reverse engineered for this challenge.

### Solving Steps 
1. View the source code of the password checker script in the terminal:
    ``` 
    cat level2.py
    ```
2. Inspecting the source code reveals the password is hardcoded in the function:
    ```
    def level_2_pw_check():
    user_pw = input("Please enter correct password for flag: ")
    if( user_pw == chr(0x64) + chr(0x65) + chr(0x37) + chr(0x36) ):
        print("Welcome back... your flag, user:")
        decryption = str_xor(flag_enc.decode(), user_pw)
        print(decryption)
        return
    print("That password is incorrect")
    ```
3. We can get the password:
    ```
    user_pw == chr(0x64) + chr(0x65) + chr(0x37) + chr(0x36) 
    ```
4. Extract the password from the ASCII values using Python:
    ```python
    print(chr(0x64) + chr(0x65) + chr(0x37) + chr(0x36))
    ```
    password = 'de76'
5. Run the password checker script:
    ```
    python3 level2.py
    ```
6. When prompt:
    ```
    Please enter correct password for flag: 
    ```
    Enter: `de76`
7. The flag will be displayed:
    ```
    Welcome back... your flag, user:
    picoCTF{tr45h_51ng1ng_489dea9a}
    ```

### Flag
    picoCTF{tr45h_51ng1ng_489dea9a}

### Notes
- chr() in python converts a hexadecimal number into its ASCII character.

- When values like chr(0x64) are added together, they form the intended password as a string.

- You can use Python to quickly evaluate character codes and test outputs.

- The script decrypts the flag using a simple XOR-based function once the correct password is entered.
---

## PW Crack 3
tag: `Medium`, `General Skills`, `Beginner picoMini 2022`, `password_cracking`, `hashing`

### Description
Can you crack the password to get the flag?
Download the password checker **here** and you'll need the encrypted **flag** and the **hash** in the same directory too.
There are 7 potential passwords with 1 being correct. You can find these by examining the password checker script.

**Hints**:
- To view the level3.hash.bin file in the webshell, do: 
    ```
    $ bvi level3.hash.bin
    ```
- To exit `bvi` type `:q` and press enter.
- The str_xor function does not need to be reverse engineered for this challenge.
### Solving Steps 
1. Open the script to see how the password verification is performed in the terminal:
    ```bash
    cat level3.py
    ```
2. From the code, observe that the script hashes the input password using MD5 and compares it to the value in `level3.hash.bin`. It also contains a hardcoded list of 7 candidate passwords:
    ```python
    pos_pw_list = ["8799", "d3ab", "1ea2", "acaf", "2295", "a9de", "6f3d"]
    ```
3. To find which password matches the hash, write a short Python script to compute each password’s MD5 hash and compare it to the hash in level3.hash.bin:
    ```python
    import hashlib
    import re

    correct_hash = open("level3.hash.bin", "rb").read()

    # Open level3.py and find the line that defines pos_pw_list
    with open("level3.py") as f:
        for line in f:
            if line.strip().startswith("pos_pw_list"):
                pw_line = line
                break

    # Extract the list of candidate passwords from that line
    pos_pw_list = eval(pw_line.split("=")[1].strip())

    # Compare each password's MD5 hash against the correct hash
    for pw in pos_pw_list:
        m = hashlib.md5()
        m.update(pw.encode())
        if m.digest() == correct_hash:
            print(f"Correct password: {pw}")
            break
    ```
4. Run the script, we will get:

    ```
    Correct password: 2295
    ```
5. Use the password to run the original script:
    ```
    python3 level3.py
    ```
6. When prompt:
    ```
    Please enter correct password for flag: 
    ```
    Enter: `2295`
7. The flag will be displayed:
    ```
    Welcome back... your flag, user:
    picoCTF{m45h_fl1ng1ng_6f98a49f}
    ```

### Flag
    picoCTF{m45h_fl1ng1ng_6f98a49f}

### Notes
- `hashlib.md5().digest()` generates the raw MD5 hash bytes of a password string.
- `bvi` is a binary editor useful for inspecting raw binary files such as `level3.hash.bin`.
- When password hashes are stored without a salt, brute forcing a small list of candidate passwords by hashing and comparison is a common cracking technique.
---

## PW Crack 4
tag: `Medium`, `General Skills`, `Beginner picoMini 2022`, `password_cracking`, `hashing`

### Description
Can you crack the password to get the flag?
Download the password checker **here** and you'll need the encrypted **flag** and the **hash** in the same directory too.
There are 100 potential passwords with only 1 being correct. You can find these by examining the password checker script.

**Hints**:
- A for loop can help you do many things very quickly.
- The str_xor function does not need to be reverse engineered for this challenge.
### Solving Steps 
1. Open the script to see how the password verification is performed in the terminal:
    ```bash
    cat level4.py
    ```
2. From the code, observe that the script hashes the input password using MD5 and compares it to the value in `level4.hash.bin`. It also contains a hardcoded list of 7 candidate passwords:
    ```python
    pos_pw_list = ["158f", "1655", "d21e", "4966", "ed69", "1010", "dded", "844c", "40ab", "a948", "156c", "ab7f", "4a5f", "e38c", "ba12", "f7fd", "d780", "4f4d", "5ba1", "96c5", "55b9", "8a67", "d32b", "aa7a", "514b", "e4e1", "1230", "cd19", "d6dd", "b01f", "fd2f", "7587", "86c2", "d7b8", "55a2", "b77c", "7ffe", "4420", "e0ee", "d8fb", "d748", "b0fe", "2a37", "a638", "52db", "51b7", "5526", "40ed", "5356", "6ad4", "2ddd", "177d", "84ae", "cf88", "97a3", "17ad", "7124", "eff2", "e373", "c974", "7689", "b8b2", "e899", "d042", "47d9", "cca9", "ab2a", "de77", "4654", "9ecb", "ab6e", "bb8e", "b76b", "d661", "63f8", "7095", "567e", "b837", "2b80", "ad4f", "c514", "ffa4", "fc37", "7254", "b48b", "d38b", "a02b", "ec6c", "eacc", "8b70", "b03e", "1b36", "81ff", "77e4", "dbe6", "59d9", "fd6a", "5653", "8b95", "d0e5"]
    ```
3. To find which password matches the hash, write a short Python script to compute each password’s MD5 hash and compare it to the hash in level4.hash.bin:
    ```python
    import hashlib
    import re

    correct_hash = open("level4.hash.bin", "rb").read()

    with open("level4.py") as f:
        for line in f:
            if line.strip().startswith("pos_pw_list"):
                pw_line = line
                break

    # Extract the list of candidate passwords from that line
    pos_pw_list = eval(pw_line.split("=")[1].strip())

    # Compare each password's MD5 hash against the correct hash
    for pw in pos_pw_list:
        m = hashlib.md5()
        m.update(pw.encode())
        if m.digest() == correct_hash:
            print(f"Correct password: {pw}")
            break
    ```
4. Run the script, we will get:

    ```
    Correct password: 8b95
    ```
5. Use the password to run the original script:
    ```
    python3 level4.py
    ```
6. When prompt:
    ```
    Please enter correct password for flag: 
    ```
    Enter: `8b95`
7. The flag will be displayed:
    ```
    Welcome back... your flag, user:
    picoCTF{fl45h_5pr1ng1ng_cf341ff1}
    ```

### Flag
    picoCTF{fl45h_5pr1ng1ng_cf341ff1}
---

## PW Crack 5
tag: `Medium`, `General Skills`, `Beginner picoMini 2022`, `password_cracking`, `hashing`

### Description
Can you crack the password to get the flag?
Download the password checker **here** and you'll need the encrypted **flag** and the **hash** in the same directory too. Here's a **dictionary** with all possible passwords based on the password conventions we've seen so far.

**Hints**:
- Opening a file in Python is crucial to using the provided dictionary.
- You may need to trim the whitespace from the dictionary word before hashing. Look up the Python string function, `strip`
- The str_xor function does not need to be reverse engineered for this challenge.
### Solving Steps 
1. We have to read the `dictionary.txt` since the file has all the possible passwords.  
2. Observe the `level5.py` code — it checks whether the MD5 hash of the input matches the one stored in `level5.hash.bin`.  
3. We write a Python script to:
    - Load the correct hash from `level5.hash.bin`  
    - Open `dictionary.txt`, read each line (each line is a candidate password)  
    - Strip any whitespace or newline characters  
    - Compute the MD5 hash of the password and compare it to the target hash  
4. Python script used:
    ```python
    import hashlib
    import re

    correct_hash = open("level5.hash.bin", "rb").read()

    with open("dictionary.txt") as f:
        for line in f:
            pw = line.strip()
            if hashlib.md5(pw.encode()).digest() == correct_hash:
                print(f"Correct password: {pw}")
                break
    ```
5. Running the script outputs:
    ```
    Correct password: 9581
    ```
6. Run the password checker:
    ```bash
    python3 level5.py
    ```
7. When prompted:
    ```
    Please enter correct password for flag:
    ```
    Enter: `9581`  
8. The script will output the decrypted flag:
    ```
    Welcome back... your flag, user:
    picoCTF{h45h_sl1ng1ng_36e992a6}
    ```

### Flag 
    picoCTF{h45h_sl1ng1ng_36e992a6}

### Notes
- `dictionary.txt` contains a full list of potential passwords; brute-forcing by hash comparison is the intended approach.  
- `hashlib.md5().digest()` produces a raw 16-byte MD5 hash that can be compared directly to the value in `level5.hash.bin`.  
- `line.strip()` is necessary to remove trailing `\n` or whitespace characters from dictionary entries.
---
