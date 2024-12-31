# [Miscellaneous] Christmas GIFt

## By: LK
## Challenge Description
<img width="323" alt="Challenge" src="https://github.com/user-attachments/assets/a3a3517e-33a0-4595-827c-268853024352">

## Write-Up
We are given a abnormally large GIF file named `gift.gif`. The challenge description stated that we should open and wait for the flag to appear.

However, after opening the GIF for some time, the graphic is changing very slowly and the flag is nowhere to be seen.

Recall that the size of the GIF is 36.6MB.

![image](https://github.com/user-attachments/assets/5816cac7-b0b7-4afb-a15e-9b821b53f57c)

This hints that it might be a super longgggggg GIF.

To investigate further, we can use video editors like ClipChamp.
>Clipchamp is a video editing software developed by Microsoft. It is a browser-based tool (accessible online) and also offers a desktop app for Windows.

![image](https://github.com/user-attachments/assets/526d85f6-e542-4cc0-b5c9-f8f68997ac3a)

As suspected, the GIF is a super long GIF with a length of more than 254 hours.
![image](https://github.com/user-attachments/assets/9eefe4d2-ea14-4f80-b246-69eac71c557a)

Let's see the last frame in the GIF by dragging the slidor to the far right.
![image](https://github.com/user-attachments/assets/299bdc98-d99c-4af1-b50b-6a0efdc8dc66)

The flag is finally revealed.
![image](https://github.com/user-attachments/assets/80beac77-7b01-433f-ba9c-6dcfc4244d84)
