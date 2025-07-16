# Section 3

## Wave a flag
tag: `Easy`, `General Skills`, `picoCTF 2021`

### Description
Can you invoke help flags for a tool or binary? **This program** has extraordinarily helpful information...

**Hints**:
- This program will only work in the webshell or another Linux computer.
- To get the file accessible in your shell, enter the following in the Terminal prompt: $ wget https://mercury.picoctf.net/static/a14be2648c73e3cda5fc8490a2f476af/warm
- Run this program by entering the following in the Terminal prompt: $ ./warm, but you'll first have to make it executable with $ chmod +x warm
- -h and --help are the most common arguments to give to programs to get more information from them!
- Not every program implements help features like -h and --help.

### Solving Steps 
1. Press **The program** to download the file `warm`.
2. Give it execute permission:
    ```bash
    chmod +x warm
    ```
3. Run with `-h` to see help text:
    ```bash
    ./warm -h
    ```
4. The program outputs:
    ```text
    Oh, help? I actually don't do much, but I do have this flag here: picoCTF{b1scu1ts_4nd_gr4vy_755f3544}
    ```

### Flag
```text
picoCTF{b1scu1ts_4nd_gr4vy_755f3544}
```

### Notes
- cat warm shows binary noise because warm is an ELF executable.
- Use ./warm -h or strings warm to extract readable strings.
- -h is a common help flag — it's a hint for interacting with binaries.
---

## Tab, Tab, Attack
tag: `Easy`, `General Skills`, `picoCTF 2021`

### Description
Using tabcomplete in the Terminal will add years to your life, esp. when dealing with long rambling directory structures and filenames: **Addadshashanammu.zip**

**Hints**:After `unzip`ing, this problem can be solved with 11 button-presses...(mostly Tab)...

### Solving Steps 
1. Press **Addadshashanammu.zip** to download the zip file.
2.  Unzip the file:
    ```bash
    unzip Addadshashanammu.zip
    cd TAddadshashanammu
    ```
3. Use `cd` + `<Tab>` to auto-complete nested directories, keep pressing `tab` to navigate until finding the file **fang-of-haynekhtnamet** at the end of the path.
4. Extract the flag using one of the following methods:
    - Using `strings` to search for readable text
        ```bash
        strings fang-of-haynekhtnamet | grep picoCTF
        ```
    - Make the file executable and run with `-h`
        ```bash
        chmod +x fang-of-haynekhtnamet
        ./fang-of-haynekhtnamet -h
        ```
5. We can get the text:
    ```
    *ZAP!* picoCTF{l3v3l_up!_t4k3_4_r35t!_6f332f10}
    ```
6. The flag is:
    ```
    picoCTF{l3v3l_up!_t4k3_4_r35t!_6f332f10}
    ```

### Flag
    picoCTF{l3v3l_up!_t4k3_4_r35t!_6f332f10}

### Notes
- This challenge demonstrates the power of Tab completion in Linux shells for navigating complex directory trees.
- `strings` is a quick way to extract readable text from ELF/binary files.
- ELF files often respond to -h with help messages, which may contain useful information or flags.
---

## Insp3ct0r
tag: `Easy`, `Web Exploitation`, `picoCTF 2019`

### Description
Kishor Balan tipped us off that the following code may need inspection: https://jupiter.challenges.picoctf.org/problem/44924/ or http://jupiter.challenges.picoctf.org:44924

**Hints**:
- How do you inspect web code on a browser?
- There's 3 parts

### Solving Steps 
1. Click the link https://jupiter.challenges.picoctf.org/problem/44924/ in the description.
2. Open Developer Tools in your browser (right-click > Inspect or press F12).
3. Look for clues in the following places:
- HTML source code (Elements tab)
- Inline script in <script> tag
- External JavaScript file (in Sources or linked in HTML)
- **The page itself says: "I used these to make this site: HTML, CSS, JS", hinting that you should inspect all three.**
4. Find the three flag segments hidden in these sources. Combine them into one flag.
5. The full flag looks like:
    ```
    picoCTF{tru3_d3t3ct1ve_0r_ju5t_lucky?f10be399}
    ```

### Flag
    picoCTF{tru3_d3t3ct1ve_0r_ju5t_lucky?f10be399}

### Notes
- This challenge teaches how to inspect web elements and understand basic client-side code.
- Developer Tools are your best friend when solving web exploitation problems.
- Always check for hidden fields, scripts, and comments in source code.
---

## strings it
tag: `Easy`, `General Skills`, `picoCTF 2019`

### Description
Can you find the flag in **file** without running it?

**Hints**:[strings](https://linux.die.net/man/1/strings)

### Solving Steps 
1. click on **file** link in the description to download the file "string"
2. Open a linux terminal.
3. Navigate to the directory where the file is located using the `cd` command.
4. Use `strings` command to fetch the flag.
    ```bash
    strings strings | grep picoCTF
    ```
5. We can fetch the flag:
    ```
    picoCTF{5tRIng5_1T_7f766a23}
    ```

### Flag
    picoCTF{5tRIng5_1T_7f766a23}

### Notes
- strings is a command-line tool that extracts human-readable text from binary files.
- It is useful for inspecting executables (such as ELF binaries) without running them.
- When combined with grep, it helps quickly filter out lines that match patterns like picoCTF.
---

## First Grep
tag: `Easy`, `General Skills`, `picoCTF 2019`

### Description
Can you find the flag in file? This would be really tedious to look through manually, something tells me there is a better way.

**Hints**:[grep](https://ryanstutorials.net/linuxtutorial/grep.php)

### Solving Steps 
1. click on **file** link in the description to download the file "file"
2. Open a linux terminal.
3. Navigate to the directory where the file is located using the `cd` command.
4. Use the `strings` command and pipe it into `grep` to search for the flag:
    ```bash
    strings file | grep picoCTF
    ```
5. The flag will be printed in the terminal output:
    ```
    picoCTF{grep_is_good_to_find_things_dba08a45}
    ```

### Flag
    picoCTF{grep_is_good_to_find_things_dba08a45}

### Notes
- `grep 'picoCTF' file` is the simplest way to find flag strings in a plain text file.
- `strings file | grep 'picoCTF'` is useful when dealing with binary files (e.g. ELF executables).
- `egrep` (or `grep -E`) supports extended regular expressions, allowing more flexible pattern matching:
    ```bash
    egrep 'picoCTF{[a-zA-Z0-9_]+}' file
    ```
- Use `grep -o 'picoCTF{[^}]*}'` to extract only the flag content without extra lines.
---

## where are the robots
tag: `Easy`, `Web Exploitation`, `picoCTF 2019`

### Description
Can you find the robots? https://jupiter.challenges.picoctf.org/problem/36474/ or http://jupiter.challenges.picoctf.org:36474

**Hints**:What part of the website could tell you where the creator doesn't want you to look?

### Solving Steps 
1. click on https://jupiter.challenges.picoctf.org/problem/36474/ link in the description.
2. Append `/robots.txt` to the end of the URL to access the site's robots exclusion file:
    ```
    https://jupiter.challenges.picoctf.org/problem/36474/robots.txt
    ```
3. In the content of the robots.txt file, look for any hidden or disallowed directories, such as:
    ```
    User-agent: *
    Disallow: /477ce.html
    ```
4. Visit the hidden path mentioned in the Disallow directive by appending it to the website:
    ```
    https://jupiter.challenges.picoctf.org/problem/36474/477ce.html
    ```
5. The page will display the flag:
    ```
    Guess you found the robots
    picoCTF{ca1cu1at1ng_Mach1n3s_477ce}
    ```

### Flag
    picoCTF{ca1cu1at1ng_Mach1n3s_477ce}

### Notes
- `robots.txt` is a publicly accessible file used to guide search engine crawlers on what directories not to index.
- It’s often overlooked, but in CTF challenges it is a classic place to hide secrets.
- Always check `/robots.txt` when doing web exploitation — it may reveal hidden paths or pages containing the flag.
---
