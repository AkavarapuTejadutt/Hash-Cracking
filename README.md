# Hash Cracking Script Documentation

## Overview

This script is a **hash-cracking tool** that attempts to find the plaintext value of hashed data using different public hash databases and services (like CMD5, MD5Hashing.net, and others). The script supports multiple hash algorithms, such as MD5, SHA1, SHA-256, SHA-384, and SHA-512.

The script works by sending hash values to online databases, which then return the corresponding plaintext (if available).

---

## Features

- **Supports Multiple Hash Functions:**
  - MD5
  - SHA1
  - SHA-256
  - SHA-384
  - SHA-512

- **Methods to Crack Hashes:**
  - CMD5 API
  - MD5Hashing WebSocket API
  - Nitrxgen Database
  - MD5Decrypt API

- **Supports Multiple Input Sources:**
  - Single Hash (`-s`)
  - Hashes from a file (`-f`)
  - Hashes from a directory (`-d`)

- **Multithreading Support:** You can control the number of threads used for cracking hashes with the `-t` argument, making it more efficient for larger numbers of hashes.

---

## Requirements

Before running the script, ensure you have the following Python libraries installed:
- `requests`
- `urllib3`
- `websocket-client`
- `concurrent.futures`

You can install them using pip:
```bash
pip install requests urllib3 websocket-client
```

---

## How to Run the Script

### 1. **Running with a Single Hash (`-s`)**

If you have a single hash and want to crack it, use the `-s` option followed by the hash value.

Example:
```bash
python Hash.py -s <your_hash_value>
```

#### Example:
```bash
python Hash.py -s 5d41402abc4b2a76b9719d911017c592
```

**Explanation:**
- `5d41402abc4b2a76b9719d911017c592` is the hash you want to crack.
- The script will automatically identify the hash type (MD5 in this case) and attempt to crack it using multiple services.

### 2. **Running with a File of Hashes (`-f`)**

If you have a file with a list of hashes, use the `-f` option and provide the file path. Each hash should be on a separate line in the file.

Example:
```bash
python Hash.py -f <file_with_hashes.txt>
```

#### Example:
```bash
python Hash.py -f hashes.txt
```

**Explanation:**
- `hashes.txt` contains the list of hash values (one per line).
- The script will read the file, crack each hash, and display the results.

### 3. **Running with Hashes in a Directory (`-d`)**

If you have a directory containing files that may have hashes, use the `-d` option followed by the directory path. The script will search for hashes within the directory and attempt to crack them.

Example:
```bash
python Hash.py -d <directory_path>
```

#### Example:
```bash
python Hash.py -d C:\path\to\directory
```

**Explanation:**
- The script will search all files in the specified directory for hashes and attempt to crack them.
- Results are saved in a file named `cracked-<directory_name>.txt`.

### 4. **Specifying the Number of Threads (`-t`)**

The `-t` option allows you to specify how many threads to use for cracking hashes. This can improve performance when dealing with multiple hashes.

Example:
```bash
python Hash.py -f hashes.txt -t 8
```

**Explanation:**
- This will use **8 threads** for cracking hashes in the file `hashes.txt`.

---

## Output

The script will output the following information:

### For Single Hashes:
If the hash is cracked successfully, it will show the hash along with its corresponding plaintext value:

```
[!] Hash function : MD5
[+] hello
```

If the hash is not found in any database:

```
[-] Hash was not found in any database.
```

### For Multiple Hashes (File or Directory):
The script will output the status of the hashes found, the progress, and any cracked hashes:

```
[!] Hashes found: 2
5d41402abc4b2a76b9719d911017c592 : hello
e99a18c428cb38d5f260853678922e03 : abc123
[!] Results saved in cracked-hashes.txt
```

The cracked hashes and their corresponding plaintext values will be saved to a file named `cracked-<input_file_name>.txt` or `cracked-<directory_name>.txt`.

---

## Troubleshooting

- **Hashes Not Cracking:** The script relies on public hash databases. If a hash is not found, it may not exist in these databases. Try using different or more common hashes.
  
- **Missing Dependencies:** If you receive errors related to missing dependencies, make sure you have installed all necessary libraries (`requests`, `urllib3`, `websocket-client`) via pip.

- **File Path Issues:** Ensure that your file or directory paths are correct. If the script can't find the file or directory, check your current working directory using `dir` (Windows) or `ls` (Linux/Mac).

---

## License

This project is open-source and available for educational use. Modify and distribute it as you wish.

---
