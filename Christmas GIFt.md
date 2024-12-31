# [Miscellaneous] Christmas GIFt

## By: LK
## Challenge Description
<img width="323" alt="Challenge" src="https://github.com/user-attachments/assets/a3a3517e-33a0-4595-827c-268853024352">

## Write-Up
The challenge presents an abnormally large GIF file named `gift.gif`. The description instructs participants to open the file and wait for the flag to appear.

![image](https://github.com/user-attachments/assets/5816cac7-b0b7-4afb-a15e-9b821b53f57c)

Upon opening the GIF, it is observed that the graphic changes very slowly, and the flag does not appear even after a significant amount of time. This behaviour, coupled with the GIF's considerable size of 36.6MB, suggests that the file might contain an unusually longggggggg sequence of frames.

To investigate further, tools such as video editors like Clipchamp can be utilised. These tools allow for a detailed analysis of the GIF's properties and content, providing the capability to navigate through its frames efficiently.
>Clipchamp is a video editing software developed by Microsoft. It is a browser-based tool (accessible online) and also offers a desktop app for Windows.

![image](https://github.com/user-attachments/assets/526d85f6-e542-4cc0-b5c9-f8f68997ac3a)

As suspected, the GIF turns out to be extremely long, with a total duration exceeding 254 hours.
![image](https://github.com/user-attachments/assets/9eefe4d2-ea14-4f80-b246-69eac71c557a)

The challenge description's suggestion to "wait for it" hints that the flag might be located in the final frames. To uncover the hidden flag, the last frame of the GIF is examined by dragging the slider to the far right.
![image](https://github.com/user-attachments/assets/299bdc98-d99c-4af1-b50b-6a0efdc8dc66)

Upon reaching the final frame, the flag is successfully revealed.
![image](https://github.com/user-attachments/assets/80beac77-7b01-433f-ba9c-6dcfc4244d84)

#### Flag: `wgmy{1eaa6da7b7f5df6f7c0381c8f23af4d3}`
