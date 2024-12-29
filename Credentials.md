# [Cryptography] Credentials

## By: LK
<img width="323" alt="Challenge" src="https://github.com/user-attachments/assets/302ec8ad-cf32-4e59-bcc6-85aa938347b8" />

## Write-Up
The `Leak_stuff.rar` file provided in the challenge contains a folder named `Leak stuff`.
![image](https://github.com/user-attachments/assets/fc227607-b717-4c05-8777-744fea91dd03)

Inside the said folder, there are 2 text files: `passwd.txt` and `user.txt`. This is likely the leaked credentials found on the black market as stated in the challenge description.
![image](https://github.com/user-attachments/assets/9b2f087d-a485-4383-bd60-2377718a9a8d)

This is what the contents of `passwd.txt` look like:

![image](https://github.com/user-attachments/assets/6f0cb28a-3bef-4ea3-889e-d23860fa784a)

Each line contains a password hash or encrypted password AKA the leaked passwords.

On the other hand, this is the contents of `user.txt`:
![image](https://github.com/user-attachments/assets/ef8589ba-3dd6-4be2-a246-aaf136ef8faf)

Each line contains a username AKA the leaked usernames.

The goal of this challenge is to find and decrypt the password for the user `osman`.

Based on the hint, each username in user.txt corresponds to the respective password in passwords.txt at the same position in the list.

A quick search reveals that the user `osman` can be found on line 337 in `user.txt`.
![image](https://github.com/user-attachments/assets/eb24456c-8446-403b-9280-6fef09a3dc7b)

Also, on line 337 of `passwd.txt`, an encrypted password was found: `ZJPB{e6g180g9f302g8d8gddg1i2174d0e212}`, which appeared suspicious as it closely matches the flag format used in Wargames.MY, specifically `WGMY{hash}`.
![image](https://github.com/user-attachments/assets/63fb94fa-5b33-4903-8a13-999aaf9a1d79)

Moving on, to determine the cypher used to encrypt the passwords, [dCode's Cipher Identifier](https://www.dcode.fr/cipher-identifier) is an excellent tool.

The results show that there is a chance that the cypher used is Caesar cypher/ROT cypher which is a monoalphabetic substitution cypher, where each letter is replaced by another letter located a little further in the alphabet (therefore shifted but always the same for the given cypher message).
![image](https://github.com/user-attachments/assets/a14cb099-cc2e-4e3a-8e5f-69e63dbcaf48)

Using the brute force function of the [Caesar Cipher Decoder](https://www.dcode.fr/caesar-cipher) in dCode, we can decrypt the osman's encrypted password easily.
![image](https://github.com/user-attachments/assets/f90f581a-d574-4792-b56d-85c92f5cdb68)

From the results obtained, a suspicious string was observed at the left shift of 3 (🠜3) or equivalently a right shift of 23 (🠞23). The string matched the expected WGMY{...} flag format, confirming the correct decryption step.

#### Flag: `WGMY{b6d180d9c302d8a8daad1f2174a0b212}`
