# [Forensics] I Cant Manipulate People

## By: LK
## Challenge Description
<img width="323" alt="Challenge" src="https://github.com/user-attachments/assets/3607e931-3a6d-47e7-a42a-51a6bf6eadc5">

## Write-Up
The objective of this challenge is to extract a hidden message from a provided PCAP file, which reportedly contains network traffic from a compromised machine. The task involves analyzing packet data to uncover the flag.

Upon opening the PCAP file in a network protocol analyser tool like `Wireshark`, various types of traffic are visible, including ICMP, DNS, TCP, UDP, and HTTP.
![image](https://github.com/user-attachments/assets/763153b0-b4fe-4f88-83e8-355ad276f782)

> Network protocol analysers like Wireshark allow for a detailed inspection of individual packets and their payloads, making it easier to identify patterns or anomalies, such as the suspicious ICMP packets in this challenge.

Focusing on ICMP packets reveals an unusual pattern: each ICMP packet contains exactly one byte of data.
> To view only ICMP packets, use the display filter in Wireshark (the 'search bar'). Typing `icmp` will isolate all ICMP traffic, making it easier to analyse the relevant packets.

The first 5 ICMP packets display the following bytes in the data section:

```57 47 4d 59 7b```

When converted to ASCII, these bytes form the string `WGMY{`. This suggests that the flag is being transmitted through the ICMP packets, with the data section holding the flag's characters.

<img width="323" alt="ICMP (Packet 1)" src="https://github.com/user-attachments/assets/c980ad2b-4020-4b67-bd57-32c49195de6b">

<img width="323" alt="ICMP (Packet 3)" src="https://github.com/user-attachments/assets/73115b70-f964-4833-a82b-40dc697590e5">

<img width="323" alt="ICMP (Packet 5)" src="https://github.com/user-attachments/assets/48b2bf03-3170-48b5-bc76-3f7e82ae02c8">

<img width="323" alt="ICMP (Packet 7)" src="https://github.com/user-attachments/assets/3a382e57-0be5-4687-b2a6-49ba085a5696">

<img width="323" alt="ICMP (Packet 9)" src="https://github.com/user-attachments/assets/474f04bc-76b6-4f75-b230-d190b75f78c7">


To efficiently extract the bytes from the ICMP packets, the `tshark` command-line tool is used. 
> <b>What is TShark?</b><br>
TShark is the command-line version of Wireshark, a powerful network protocol analyzer. It allows users to capture and analyze network traffic directly from the terminal. TShark is particularly useful for scripting and automating packet analysis, especially when handling large PCAP files. By leveraging its robust filtering and field extraction capabilities, TShark simplifies complex tasks like isolating specific protocols or extracting payload data.

The following command is executed:

```tshark -r traffic.pcap -Y icmp -T fields -e data > icmp_payloads_hex.txt```

> <b> Explanation of the Command:</b><br>
-r traffic.pcap: Specifies the input file, in this case, traffic.pcap.<br>
-Y icmp: Filters the packets to include only ICMP traffic.<br>
-T fields: Specifies that the output should include only specific fields.<br>
-e data: Extracts the data field, which contains the payload of the ICMP packets.<br>
\> icmp_payloads_hex.txt: Redirects the extracted data into a text file named icmp_payloads_hex.txt.

As a result of the above command, the `icmp_payloads_hex.txt` file will contain the following hexadecimal values:

```57
47
4d
59
7b
31
65
33
62
37
31
64
35
37
65
34
36
36
61
62
37
31
62
34
33
63
32
36
34
31
61
34
62
33
34
66
34
7d
```

As the values extracted from the ICMP packets are in hexadecimal, they will need to be converted to ASCII before the flag can be obtained.

The conversion can be done using a tool like [CyberChef](https://cyberchef.org).
>CyberChef is an online tool designed for analyzing and manipulating data. It supports various operations like encoding, decoding, encryption, decryption, and file conversions.

The "From Hex" operation translates the said data into the following flag:
![image](https://github.com/user-attachments/assets/2d9584b3-c1c9-43da-9eb0-fb7f134a99b0)

####Flag:`WGMY{1e3b71d57e466ab71b43c2641a4b34f4}`
