# [Forensics] Unwanted Meow

## By: LK
## Challenge Description
<img width="323" alt="Challenge" src="https://github.com/user-attachments/assets/09a10925-cdcf-4d56-82a4-f80d8ce8cbc8" />

## Write-Up
The goal of this challenge is to recover the 'shredded' (corrupted) image file which contains the flag.

We are given a file named `flag.shredded`.

The first step in challenges like this is to identify the attached file type so that we can further find out what's wrong with the file.
> Often, files in CTFs are not labelled with their file types correctly. It's always good to double check!

To do this, we can use the `file` command in Unix-like machines or use an online file checker like [CheckFileType](https://www.checkfiletype.com/).
>The `file` command is a Linux/Unix command-line utility used to determine the type of a file based on its content, rather than its filename or extension. It is very helpful when working with unknown or proprietary file formats.
>
>Basic syntax:
>
>file [options] \<filename>

![image](https://github.com/user-attachments/assets/bb6792e4-db10-4577-83a5-34d10b57e6a5)

The results of the file check show that the file is likely a JPEG image file.
![image](https://github.com/user-attachments/assets/ed387c8d-5be4-45d4-b8c0-6975a1e0c72e)

Let's change the file extension to JPEG and try to open the image. The image failed to open.
![image](https://github.com/user-attachments/assets/56ea5ab3-3afa-4189-a2b7-151c54e1f9ee)

Moving forward, we can check the file data to see what's wrong. We can use a hex (hexadecimal) editor like HxD to do this. A hex editor is a software tool that allows users to view and edit the raw binary data of files, disk sectors, or memory. It displays this data in hexadecimal (base 16) format, alongside an ASCII or text representation, making it easier to interpret and manipulate.
>HxD is a popular, free hex editor for Windows. It allows users to view, edit, and analyze the raw data of files and disk sectors at the binary level.
<img width="500" alt="Screenshot 2024-12-30 225451" src="https://github.com/user-attachments/assets/ca8e1fd6-3e8c-4111-b505-fc322b1bc130" />

Going through the file contents in HxD, we can see some weird strings (`meow`) in the file contents. They are inserted between words as well like `rdf:Descmeowription`.

This is definitely very weird and suspicious. Let's remove all the `meow`s with the replace function in HxD and save it.
![image](https://github.com/user-attachments/assets/5d706a24-9f6d-481c-801c-93e3937018b3)
>Click "OK" to proceed with the HxD replace operation when prompted to continue.
>
><img width="200" src="https://github.com/user-attachments/assets/cc74bd46-eaa0-4946-b35d-6395c21295f9">

![image](https://github.com/user-attachments/assets/5814c1a7-adb7-40fa-8a1c-3fb195fe33cb)


Let's check if the image can be opened once again.
![1flag shredded](https://github.com/user-attachments/assets/e2dc4b9f-2121-4a0b-a2f3-5e8d37129a71)

We can now open the image and see a flag. However, the image and the middle part of the flag are still distorted.

Let's go through the file contents again to see if we missed anything.
![image](https://github.com/user-attachments/assets/0190cc58-eeb3-4f9a-9606-345b55de7f52)

There was some `meow`s that we missed. Checking the original file again, this is because the file data had strings of `memeowow` so when one `meow` was removed. It became `meow` again.
![image](https://github.com/user-attachments/assets/96d38bfd-1fde-4218-abcb-279371f48ab6)

![image](https://github.com/user-attachments/assets/443c7993-f4e0-45da-a85e-faebbabebd3b)

Let's remove these last `meow`s, save and open the image file again.

This time, the flag is shown completely.
![flag_shredded](https://github.com/user-attachments/assets/a986e52c-f72c-47ba-ad33-02db70cd13c1)

#### Flag: `WGMY{4a4be40c96ac6314e91d93f38043a634}`
