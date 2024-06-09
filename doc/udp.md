# <div align="center">How To Display Frame In The Real-Time (via UDP)</div>

It is the same way to cross-compile your project, like selecting stream mode. After compiling the project by executing the script named `udp.sh`, you will get the `build` folder in the project named `transfer_model`.

![](../img/udp-pipeline.png)

<details open>
<summary>Compile</summary>

```shell
sh /udp.sh transfer_model
```

After the build is completed, you can just put the executable files into NFS sharing folder (`/mnt` on the board) to see the detection result.

```shell
# Remember to execute the files on the board
./yolov3tiny network_binary.nb
```

</details>

<details open>
<summary>UDP Server</summary>

There is one last step to do. Before starting, clone the repository first.

```shell
# This command will require you to enter a key to access. Please contact us, and we will provide the key for you.
git clone https://github.com/InstAI-Co/Realtek-RTS3916n-Display-Multiple-Image.git
```

<!-- We suggest you use the `pyenv` tool to set up your environment. Remember to install Python version `3.10.12` and follow the command below."

```shell
python3 -m venv myenv
source myenv/bin/activate
pip install --upgrade pip==24.0
pip install -r requirements.txt 
```

Now, just execute the code to receive an image from the board.

```shell
# For additional information, refer to README.md in the repository where we cloned it.
python src/udp-server.py <IP> <PORT> <RESIZE_WIDTH> <RESIZE_HEIGHT>
``` -->

</details>

Congratulations! You have completed this tutorial. You can refer to other documents below:

- [How To Excute the Inference](../doc/inference.md)