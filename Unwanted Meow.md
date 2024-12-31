# [Forensics] Unwanted Meow

## By: LK
## Challenge Description
<img width="323" alt="Challenge" src="https://github.com/user-attachments/assets/09a10925-cdcf-4d56-82a4-f80d8ce8cbc8" />

## Write-Up
The goal of this challenge is to recover the 'shredded' (corrupted) image file which contains the flag.

For this challenge, a file named `flag.shredded` is provided.
![image](https://github.com/user-attachments/assets/b94a7ed9-e573-4a53-a962-5f9e334e54e8)

The first step in a challenge like this is to determine the type of the provided file. This helps in identifying its structure and understanding what might be wrong with it, enabling further analysis.
> Often, files in CTFs are not labelled with their file types correctly. It's always good to double check!

To do this, the `file` command in Unix-like systems can be used, or alternatively, an online file identification tool like [CheckFileType](https://www.checkfiletype.com/) can be utilised as well.
>The `file` command is a Linux/Unix command-line utility used to determine the type of a file based on its content, rather than its filename or extension. It is very helpful when working with unknown or proprietary file formats.
>
>Basic syntax:
>
>file [options] \<filename>

<img width="400" src="https://github.com/user-attachments/assets/bb6792e4-db10-4577-83a5-34d10b57e6a5">

The results of the file check show that the file is most likely a JPEG image file.
<img width="400" src="https://github.com/user-attachments/assets/ed387c8d-5be4-45d4-b8c0-6975a1e0c72e">

Thus, an attempt is made to open the image by changing the file extension to `.jpeg`, but as expected for a medium difficulty challenge, it fails to open.

![image](https://github.com/user-attachments/assets/56ea5ab3-3afa-4189-a2b7-151c54e1f9ee)

Moving forward, the file data is examined to uncover what might be wrong. This can be done using a hex (hexadecimal) editor like HxD. A hex editor is a software tool that allows users to view and edit the raw binary data of files, disk sectors, or memory. It displays this data in hexadecimal (base 16) format, alongside an ASCII or text representation, making it easier to interpret and manipulate.
>HxD is a popular, free hex editor for Windows. It allows users to view, edit, and analyze the raw data of files and disk sectors at the binary level.
<img width="500" alt="Screenshot 2024-12-30 225451" src="https://github.com/user-attachments/assets/ca8e1fd6-3e8c-4111-b505-fc322b1bc130" />

Examining the file contents in HxD reveals peculiar strings (`meow`) scattered throughout the data. These strings are even embedded within words, such as `rdf:Descmeowription`.

![image](https://github.com/user-attachments/assets/5d706a24-9f6d-481c-801c-93e3937018b3)

This is definitely very weird and suspicious. To address this, all instances of meow are removed using the replace function in HxD, and the file is saved with the modifications.
>Click "OK" to proceed with the HxD replace operation when prompted to continue.
>
><img width="200" src="https://github.com/user-attachments/assets/cc74bd46-eaa0-4946-b35d-6395c21295f9">

<img width="300" src="https://github.com/user-attachments/assets/5814c1a7-adb7-40fa-8a1c-3fb195fe33cb">

333 instances of "meow"s were removed and the file is saved again. 

Then, an attempt to open the file again was made to check if the image is now fixed.
![1flag shredded](https://github.com/user-attachments/assets/e2dc4b9f-2121-4a0b-a2f3-5e8d37129a71)

The image opens this time, revealing a flag. However, parts of the image, particularly the middle section of the flag, are still distorted.

To investigate further, the file contents are revisited in HxD to identify any overlooked anomalies.It turns out some `meow`s were missed.
![image](https://github.com/user-attachments/assets/0190cc58-eeb3-4f9a-9606-345b55de7f52)

Upon closer examination of the original file, the issue becomes apparent: certain strings were written as `memeowow`. When one meow was removed, it left behind another `meow`.
![image](https://github.com/user-attachments/assets/443c7993-f4e0-45da-a85e-faebbabebd3b)

To solve this, all `meow` strings are removed again. After saving the changes, the image file is reopened for verification.

<img width="300" src="https://github.com/user-attachments/assets/96d38bfd-1fde-4218-abcb-279371f48ab6">

This time, the flag is shown completely.

![flag_shredded](https://github.com/user-attachments/assets/a986e52c-f72c-47ba-ad33-02db70cd13c1)

#### Flag: `WGMY{4a4be40c96ac6314e91d93f38043a634}`
