# <div align="center">How To Display Frame In The Real-Time</div>

There are two different ways to display the frames in the window, and the list below is our main method to transport the image, as follows:

- NFS
- UDP

## <div align="center">How to Start</div>

We provide another repository containing more detailed information. Inside, there is a README.md file that describes how to use these files.

<details open>
<summary>Clone</summary>

```shell
git clone https://github.com/InstAI-Co/Realtek-RTS3916n-Display-Multiple-Image.git
```

Username: `InstAI-Co`

Token:

`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`

After setting up the environments, you can select one of the modes to use.

</details>

<details open>
<summary>Usage</summary>

- NFS

```shell
python src/display-real-time.py path/to/stream/image/
```

Since the NFS mode will generate multiple images in the common folder, it means that when the detected frame is saved in bitmap format, the computer-side will capture the latest frame and display it in the window to simulate real-time.

- UDP

```shell
python src/udp-server.py <IP> <PORT>
```

This is an efficient way to display the frames because it provides an easy interface to capture the frames sent by the Realtek EVB. It also shows low latency compared with NFS-based transport.

Congratulations! You have completed this tutorial. You can refer to other documents below:

- [Connect To Realtek Board](./connect_board.md)
- [How To Excute the Inference](./inference.md)

</details>
