# 🔐 Week 3: Password Cracking and Security Assessment

**Project:** Cybersecurity Internship – Practical Tasks  
**Tasks:** W3 – Password Cracking with John the Ripper · Password Cracking with Networkwalks Tools  
**Environment:** Ubuntu Linux + Oracle VirtualBox + Kali Linux + Windows  
**Category:** Cybersecurity / Ethical Hacking / Password Security

---

## 📌 1. Project Overview

This week focuses on password security and password recovery techniques using two different methods.

The objective is to understand how password-protected files work, how password hashes can be extracted, and how password-cracking tools attempt to recover the original password.

Two approaches were used:

- **Method 1 – John the Ripper (Kali Linux):** Extracting the password hash from an encrypted PDF using `pdf2john`, then using John the Ripper with the RockYou wordlist to recover the password.
- **Method 2 – Networkwalks Online Tools:** Using the Networkwalks Hash Calculator to extract the PDF hash, then submitting the hash to the Networkwalks Password Cracker to recover the password.

The laboratory uses the provided file `My Locked PDF1.pdf`.

Both methods demonstrate how weak or common passwords can be recovered and why strong passwords are essential for protecting sensitive files.

---

## 🎯 2. Objectives

- Understand the concept of password hashing and password-protected files.
- Learn how to extract a password hash from an encrypted PDF.
- Use John the Ripper to perform dictionary-based password cracking.
- Use the RockYou wordlist to test commonly used passwords.
- Explore online password-cracking tools provided by Networkwalks.
- Compare a local password-cracking tool with browser-based tools.
- Verify the recovered password by opening the protected PDF.
- Understand the importance of strong passwords and secure file protection.
- Document the process with commands, results, and screenshots.

---

## 💻 3. Environment

| Component | Configuration |
|---|---|
| Host Operating System | Ubuntu Linux |
| Virtualization Software | Oracle VirtualBox |
| Guest Operating System | Kali Linux (64-bit) |
| Additional Environment | Windows Laptop |
| Password Cracking Tool | John the Ripper |
| John Version | 1.9.0-jumbo-1+bleeding-aec1328d6c |
| Hash Extraction Tool | pdf2john |
| Wordlist | RockYou |
| Online Hash Calculator | Networkwalks |
| Online Password Cracker | Networkwalks |
| Target File | My Locked PDF1.pdf |
| File Type | Password-protected PDF |

---

## 🗂️ 4. Tasks Summary

| Module | Task | Tool | Status |
|---|---|---|---|
| W3 | Verify password-cracking tool installation | John the Ripper | ✅ Completed |
| W3 | Locate PDF hash extraction script | pdf2john | ✅ Completed |
| W3 | Extract PDF password hash | pdf2john | ✅ Completed |
| W3 | Prepare password dictionary | RockYou | ✅ Completed |
| W3 | Perform dictionary attack | John the Ripper | ✅ Completed |
| W3 | Recover PDF password | John the Ripper | ✅ Completed |

---

# ⚙️ 5. Implementation

## 🔹 Method 1: Password Cracking with John the Ripper (Kali Linux)

### Step 1: Verify John the Ripper Installation

Command:

```bash
/usr/share/kali-menu/helper-scripts/john.sh
```

Result:

- John the Ripper was successfully launched.
- Version: `1.9.0-jumbo-1+bleeding-aec1328d6c`.
- Architecture: Linux 64-bit x86_64.
- CPU optimization: AVX2 and OpenMP.

### Step 2: Locate pdf2john

The `pdf2john` utility extracts password hashes from protected PDF files.

Command:

```bash
locate pdf2john
```

Result:

```text
/usr/bin/pdf2john
/usr/share/john/pdf2john.pl
```

The utility was successfully located and ready to use.

### Step 3: Locate the PDF File

The provided PDF files were stored in the Kali Downloads directory.

Command:

```bash
ls /home/anil/Téléchargements/
```

Available files:

```text
My Locked PDF1.pdf
My Locked PDF2.pdf
My Locked PDF3.pdf
```

The first file was selected for the exercise:

`My Locked PDF1.pdf`

### Step 4: Extract the PDF Hash

The `pdf2john` utility was used to extract the password hash from the protected PDF.

Command:

```bash
pdf2john "/home/anil/Téléchargements/My Locked PDF1.pdf" > hash.txt
```

The extracted hash was saved in `hash.txt`.

To display the extracted hash:

```bash
cat hash.txt
```

Result:

A long hash line containing the PDF encryption information was generated successfully.

The hash starts with the PDF format identifier and contains the information required by John the Ripper.

### Step 5: Prepare the RockYou Wordlist

The RockYou dictionary was used to perform a dictionary attack.

First, the available wordlist was checked:

```bash
ls -lh /usr/share/wordlists/rockyou.txt*
```

The compressed wordlist was extracted using:

```bash
sudo gzip -dk /usr/share/wordlists/rockyou.txt.gz
```

The resulting dictionary was available at:

```text
/usr/share/wordlists/rockyou.txt
```

### Step 6: Execute the Dictionary Attack

John the Ripper was executed using the extracted hash and RockYou dictionary.

Command:

```bash
john --wordlist=/usr/share/wordlists/rockyou.txt hash.txt
```

Result:

```text
Using default input encoding: UTF-8
Loaded 1 password hash (PDF [MD5 SHA2 RC4/AES 32/64])
Cost 1 (revision) is 4 for all loaded hashes
Will run 3 OpenMP threads

good-luck (/home/anil/Téléchargements/My Locked PDF1.pdf)

1g 0:00:00:14 DONE
Session completed.
```

John the Ripper successfully recovered the password.

### Step 7: Display the Recovered Password

Command:

```bash
john --show hash.txt
```

Result:

```text
/home/anil/Téléchargements/My Locked PDF1.pdf:good-luck
```

**Recovered password: `good-luck`**

Execution time: approximately 14 seconds.

The password was found because it was included in the RockYou dictionary.

### Step 8: Verify the Password

The recovered password should be tested by opening the protected PDF.

Command:

```bash
evince "/home/anil/Téléchargements/My Locked PDF1.pdf"
```

When prompted, enter:

```text
good-luck
```

The PDF should open if the recovered password is correct.

**Verification status:** To be confirmed with a screenshot.

---

## 🔹 Method 2: Password Cracking with Networkwalks Tools

### Background

Networkwalks provides two online tools for understanding password recovery:

1. **Hash Calculator:** Extracts the password hash from a protected PDF.
2. **Password Cracker:** Attempts to recover the original password from the extracted hash.

Both tools operate directly in a web browser and do not require installing password-cracking software.

### Step 1: Download the Encrypted PDF

The protected PDF was downloaded from the Networkwalks laboratory page.

Lab page:

https://networkwalks.com/project-task-lab-password-cracking-with-networkwalks-tools/

Target file:

```text
My Locked PDF1.pdf
```

### Step 2: Open the Networkwalks Hash Calculator

Open the following website:

https://networkwalks.com/hash-calculator/

The Hash Calculator is used to extract the hash from the encrypted PDF.

### Step 3: Upload the Protected PDF

Upload `My Locked PDF1.pdf` to the Hash Calculator.

The tool processes the PDF and generates its password hash.

The generated hash starts with:

```text
$pdf$
```

### Step 4: Copy the Complete Hash

Copy the entire generated hash.

It is important to copy the complete value without removing or modifying any characters.

### Step 5: Open the Networkwalks Password Cracker

Open:

https://networkwalks.com/password-cracker/

This tool is used to attempt password recovery from the extracted hash.

### Step 6: Submit the Hash

Paste the complete hash into the Password Cracker.

Start the password-cracking process.

The tool attempts different password candidates until it finds a matching password or exhausts its available candidates.

### Step 7: Retrieve the Password

Wait for the cracking process to finish.

The recovered password should appear on the screen if the tool successfully finds a match.

Expected password according to the laboratory instructions:

```text
password1
```

**Note:** The actual result must be confirmed by performing the exercise. Do not assume that the online tool returned the expected password without verification.

### Step 8: Verify the Password

Open the protected PDF and enter the recovered password.

If the password is correct, the document will open successfully.

**Verification status:** To be completed.

---

## 📊 6. Comparison Between Both Methods

| Criteria | John the Ripper | Networkwalks Tools |
|---|---|---|
| Execution Environment | Kali Linux | Web Browser |
| Hash Extraction | pdf2john | Hash Calculator |
| Password Cracking | John the Ripper | Password Cracker |
| Wordlist | RockYou | Managed by online tool |
| Installation | Required | Not required |
| Internet Connection | Not required for local cracking | Required |
| Customization | High | Depends on online tool |
| Result | Password recovered | To be tested |

### Main Differences

**John the Ripper:**
- Runs locally on Kali Linux.
- Supports different hash formats.
- Allows custom dictionaries and cracking configurations.
- Provides control over the cracking process.

**Networkwalks Tools:**
- Runs directly in a browser.
- Simplifies hash extraction and password recovery.
- Does not require local installation.
- Provides a more beginner-friendly experience.

---

## 📸 7. Evidence and Screenshots

The following screenshots should be added to document the practical work.

### Method 1 – John the Ripper

| # | Screenshot | Description |
|---|---|---|
| 1 | John Installation | John the Ripper version and installation |
| 2 | pdf2john Location | Location of the PDF hash extraction utility |
| 3 | PDF Files | List of downloaded protected PDFs |
| 4 | Hash Extraction | Execution of pdf2john |
| 5 | Extracted Hash | Contents of hash.txt |
| 6 | RockYou Wordlist | Decompression of rockyou.txt.gz |
| 7 | Dictionary Attack | John the Ripper execution |
| 8 | Recovered Password | john --show hash.txt |
| 9 | PDF Verification | Successfully opening the PDF |

### Method 2 – Networkwalks

| # | Screenshot | Description |
|---|---|---|
| 1 | Lab Page | Networkwalks password-cracking laboratory |
| 2 | Hash Calculator | Hash Calculator interface |
| 3 | PDF Upload | Uploading My Locked PDF1.pdf |
| 4 | Extracted Hash | Generated PDF hash starting with $pdf$ |
| 5 | Password Cracker | Password Cracker interface |
| 6 | Hash Submission | Submitting the extracted hash |
| 7 | Cracking Result | Recovered password displayed by the tool |
| 8 | PDF Verification | Opening the PDF with the recovered password |

---

## 🧠 8. What I Learned

During this laboratory, I learned:

- How password-protected PDF files use encryption to protect their contents.
- The difference between a password and its extracted hash representation.
- How to extract a PDF password hash using pdf2john.
- How to use John the Ripper to perform dictionary-based password attacks.
- How to prepare and use the RockYou wordlist.
- How to recover a weak password in approximately 14 seconds.
- How online tools can simplify the hash extraction and password recovery process.
- The differences between local and browser-based password-cracking tools.
- Why common passwords are vulnerable to dictionary attacks.
- Why strong, unique passwords are important for protecting sensitive documents.

---

## 🔐 9. Security and Ethical Considerations

- Password-cracking activities were performed for educational purposes.
- Only the PDF files provided for the laboratory were used.
- The tools were used within an authorized learning environment.
- Recovered passwords should not be used to access files without permission.
- Password hashes should be treated as sensitive information.
- Online hash calculators and password crackers may receive uploaded documents or hashes. Only use files you are authorized to share with the service.
- Strong passwords should be long, unique, and difficult to guess.
- Dictionary attacks demonstrate why passwords based on common words and predictable patterns are not secure.

---

## 🚀 10. Next Steps

- Complete the password verification for `My Locked PDF1.pdf`.
- Perform the Networkwalks method and document its actual result.
- Compare the passwords recovered by both methods.
- Test the remaining laboratory PDFs if required by the instructor.
- Explore additional John the Ripper options and wordlists in an authorized lab.
- Study password security best practices, including password managers and multi-factor authentication.
- Explore the optional AI-assisted password-cracking laboratory using Claude and Hexstrike MCP.
- Study Web Application Security through the Mediroza Hospital Patient Portal laboratory.

---

## 📚 11. References

- [John the Ripper – Official Website](https://www.openwall.com/john/)
- [John the Ripper – Documentation](https://www.openwall.com/john/doc/)
- [Kali Linux](https://www.kali.org/)
- [RockYou Wordlist](https://github.com/brannondorsey/naive-hashcat)
- [Networkwalks – Password Cracking Lab](https://networkwalks.com/project-task-lab-password-cracking-with-networkwalks-tools/)
- [Networkwalks – Hash Calculator](https://networkwalks.com/hash-calculator/)
- [Networkwalks – Password Cracker](https://networkwalks.com/password-cracker/)

---

## 👤 12. Task Information

| Field | Details |
|---|---|
| Internship Task | Week 3 |
| Main Topic | Password Cracking |
| Method 1 | John the Ripper + pdf2john |
| Method 2 | Networkwalks Hash Calculator + Password Cracker |
| Host OS | Ubuntu Linux / Windows |
| Virtualization | Oracle VirtualBox |
| Guest OS | Kali Linux |
| Target File | My Locked PDF1.pdf |
| Recovered Password (Method 1) | good-luck |
| Method 1 Status | ✅ Completed |
| Method 2 Status | ⏳ To be completed |
| Overall Status | In Progress |
| Repository | GitHub |

---

**This repository documents the password security and password recovery exercises completed during Week 3 of the cybersecurity internship. It demonstrates two approaches to password cracking and highlights the importance of strong passwords in protecting sensitive files.**
