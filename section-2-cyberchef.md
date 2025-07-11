# Section 2 (CyberChef)

## Mod 26  
tag: Easy, Cryptography, picoCTF 2021

### Description  
Cryptography can be easy, do you know what ROT13 is?  

`cvpbPGS{arkg_gvzr_V'yy_gel_2_ebhaqf_bs_ebg13_jdJBFOXJ}`

### Solving Steps  
1. Recognize that the string uses **ROT13**, a basic Caesar cipher where each letter is rotated by 13 places.
2. Go to the online tool [CyberChef](https://gchq.github.io/CyberChef/).
3. In the **"Recipe"** section, add the operation `ROT13`.
4. Paste the ciphertext:
    ```
    cvpbPGS{arkg_gvzr_V'yy_gel_2_ebhaqf_bs_ebg13_jdJBFOXJ}
    ```
5. The decoded output will appear:
    ```
    picoCTF{next_time_I'll_try_2_rounds_of_rot13_wqWOSBKW}
    ```

### Flag  
    picoCTF{next_time_I'll_try_2_rounds_of_rot13_wqWOSBKW}


### Notes  
- **ROT13** is a Caesar cipher with a fixed shift of 13, since the alphabet has 26 letters, applying ROT13 twice returns the original text.
- Tools like [CyberChef](https://gchq.github.io/CyberChef/) make it easy to decode simple ciphers.
---


## Warmed Up
tag: Easy, General Skills, picoCTF 2019

### Description
What is 0x3D (base 16) in decimal (base 10)?

**Hint**:Submit your answer in our flag format. For example, if your answer was '22', you would submit 'picoCTF{22}' as the flag.

### Solving Steps  
1. Recognize that `0x3D` is a hexadecimal (base 16) number.
2. Convert it to decimal using a calculator or programming language:
    - In Bash:
        ```bash
        echo $((0x3D))
        ```
    - In Python:
        ```python
        int("0x3D", 16)
        ```
3. You will get:
    ```
    61
    ```
4. Wrap it in the flag format:
    ```
    picoCTF{61}
    ```

### Flag  
    picoCTF{61}
    
### Notes  
- `0x` is a prefix that indicates a hexadecimal number.
- You can convert hex to decimal using:
  - Bash: `echo $((0xVALUE))`
  - Python: `int("0xVALUE", 16)`
  - Online tools like CyberChef or rapidtables.com
---

## 2Warm
tag: Easy, General Skills, picoCTF 2019

### Description
Can you convert the number 42 (base 10) to binary (base 2)?

**Hint**:Submit your answer in our competition's flag format. For example, if your answer was '11111', you would submit 'picoCTF{11111}' as the flag.

### Solving Steps
1. Recognize that this is a base conversion: **decimal to binary**.
2. Use a tool or command to convert:
    - In Bash:
        ```bash
        echo "obase=2; 42" | bc
        ```
    - In Python:
        ```python
        bin(42)
        # Output: '0b101010'
        ```
        Then remove the `0b` prefix → `101010`
    - Use an online converter (e.g. https://www.rapidtables.com/convert/number/decimal-to-binary.html)

3. The result is:
    ```
    101010
    ```

4. Wrap it in the flag format:
    ```
    picoCTF{101010}
    ```

### Flag  
    picoCTF{101010}
    
### Notes  
- This challenge tests basic understanding of number base conversions.
- In Bash, `bc` is a calculator that can change number bases (`obase` = output base).
- In Python, `bin(n)` returns a string in the format `'0bXXXX'`.
- Binary (base 2) only contains digits `0` and `1`, and is commonly used in low-level programming and CTF challenges.
---

## Bases
tag: Easy, General Skills, picoCTF 2019

### Description
What does this bDNhcm5fdGgzX3IwcDM1 mean? I think it has something to do with bases.

**Hint**:Submit your answer in our flag format. For example, if your answer was 'hello', you would submit 'picoCTF{hello}' as the flag.

### Solving Steps
1. Recognize that the string `bDNhcm5fdGgzX3IwcDM1` is likely **base64 encoded**.
2. Use a decoding tool:
    - In Bash:
        ```bash
        echo bDNhcm5fdGgzX3IwcDM1 | base64 -d
        ```
    - In Python:
        ```python
        import base64
        base64.b64decode("bDNhcm5fdGgzX3IwcDM1").decode()
        ```
    - Use an online tool like [CyberChef](https://gchq.github.io/CyberChef/) and apply the **From Base64** operation.

3. Decoded result:
    ```
    l3arn_th3_r0p35
    ```

4. Wrap it in the flag format:
    ```
    picoCTF{l3arn_th3_r0p35}
    ```

### Flag  
    picoCTF{l3arn_th3_r0p35}

### Notes  
- The string was base64 encoded, a common encoding format that uses A-Z, a-z, 0-9, `+`, `/`, and `=` padding.
- This kind of challenge tests your ability to recognize encoded formats and use the right tools to decode them.
- In Linux, `base64` is a built-in utility and very useful for quick decoding.
---
