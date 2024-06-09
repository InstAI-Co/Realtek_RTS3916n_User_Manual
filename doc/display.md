# <div align="center">How To Display Frame In The Real-Time</div>

There are two different ways to display the AI model inference result frames in the window in real-time, and the following list is shows our methods of transporting the image with bounding boxes from the board to display window on PC:

- NFS
- UDP

## <div align="center">How to Start</div>

We provide another repository containing more detailed information. Inside, there is a README.md file that describes how to use these files.

<details open>
<summary>Clone</summary>

```shell
# This command will require you to enter a key to access. Please contact us, and we will provide the key for you.
git clone https://github.com/InstAI-Co/Realtek-RTS3916n-Display-Multiple-Image.git
```

After setting up the environments, you can select one of the modes to use.

</details>

<details open>
<summary>Usage</summary>

### NFS

```shell
python src/display-real-time.py path/to/stream/image/
```

Since the NFS mode will generate multiple images in the sharing folder, it means that whenever the AI model inference result frame is saved in the folder (bitmap format), the PC-side will capture the latest frame and display it in the window to achieve real-time AI inference.

### UDP

```shell
python src/udp-server.py <IP> <PORT> <RESIZE_WIDTH> <RESIZE_HEIGHT>
```

This is an efficient way to display the frames because it provides an event-triggered mechanism (via UDP) to  transfer the AI inferenced results frames from the Realtek EVB to PC, which shows low latency compared with NFS-based transport.

</details>

Congratulations! You have completed this tutorial.
