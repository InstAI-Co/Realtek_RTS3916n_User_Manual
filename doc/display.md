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

It is the same way to cross-compile your project, like selecting stream mode. After compiling the project by executing the script named `udp.sh`, you will get the `build` folder in the project named `transfer_model`.

![](../img/udp-pipeline.png)

<details open>
<summary>Download Repository Realtek_RTS3916n_UDP_Inference from Git for the First Time</summary>

Download source code for compiling UDP client program executes on RTS3916n in Docker container `realtek_rts3916n` for the first time.

<b>Warning</b>: this process requires InstAI's permission and the key for accessing Git Repo `Realtek_RTS3916n_UDP_Inference`.

```shell
cd /realhome
git clone https://github.com/InstAI-Co/Realtek_RTS3916n_UDP_Inference.git
```

</details>

<details open>
<summary>Compile</summary>

```shell
cd Realtek_RTS3916n_UDP_Inference
make
```

After the build is completed, put all of the contents in folder `build/`  into NFS sharing folder (`/mnt` on the board) to see the detection result.

Argument `[UDP server IP]` is the PC IP address that runs UDP server python program, e.g. `192.168.1.8`. Refer to the next section to set up the environment on PC. Both PC and RTS3916n must be connected with Ethernet cable to transmit camera images and inference results.

```shell
# Remember to execute the files on the board
./yolov3tiny network_binary.nb [UDP server IP]
```

</details>

<details open>
<summary>UDP Server</summary>

There is one last step to do. Before starting, clone the repository first.

```shell
cd Realtek-RTS3916n-Display-Multiple-Image
```

We suggest you use the `pyenv` tool to set up your environment. Remember to install Python version `3.10.12` and follow the command below.

```shell
python3 -m venv myenv
source myenv/bin/activate
pip install --upgrade pip==24.0
pip install -r requirements.txt 
# remove default numpy v2, and install numpy v1
pip uninstall numpy
pip install numpy==1.26.4
```

Now, just execute the code to receive an image from the board.

```shell
python src/udp-server.py <IP> <PORT> <RESIZE_WIDTH> <RESIZE_HEIGHT>
```

e.g. set up UDP server on local PC, with display window resolution 640x480

```shell
python src/udp-server.py 0.0.0.0 8080 640 480
```

This is an efficient way to display the frames because it provides an event-triggered mechanism (via UDP) to  transfer the AI inferenced results frames from the Realtek EVB to PC, which shows low latency compared with NFS-based transport.

</details>

Congratulations! You have completed this tutorial.
