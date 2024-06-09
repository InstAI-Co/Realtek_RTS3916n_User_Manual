# <div align="center">Connect Realtek Board with PC</div>

<div align="center">
    <img src="../img/minicom.png" alt="minicom">
</div>

## <div align="center">Minicom</div>

***Minicom*** is a tool on PC, used to communicate with the Realtek board. After the package is installed, power on the board and also use a 'USB to TTL' chip to receive data from the board. (refer to Realtek Board - Wiring part)

<details open>
<summary>Install</summary>

```shell
sudo apt install minicom
```

After install, you can execute following command and select **Serial port setup** to set the Bps/Par/Bits to **57600 8N1**:

```shell
sudo minicom -s
```

<div align="center">
    <img src="../img/minicom_setting.png" width="400">
</div>

</details>

<details open>
<summary>Usage</summary>

```shell
sudo minicom -D /dev/ttyUSB0
```

<!-- The '/dev/ttyUSB0' is a 'USB to TTL' chip. If you want to ensure which device is yours, you can use the command "sudo dmesg --follow" to check when the chip is connecting to your computer. -->

`/dev/ttyUSB0` is the device path for connected `USB to TTL` chip. If you want to identify which path is USB to TTL chip that has been connected, you can use the command `sudo dmesg --follow` to check the messages and find the device path when the chip connects to your computer.

</details>

## <div align="center">NFS</div>

***NFS*** is used to share files and folders from your computer to the Realtek Board. After we complete converting and cross-compiling the YOLOv3-tiny model and generate the model executable, NFS tool allows us to transfer it from PC to the Board before performing inference step.

<details open>
<summary>Install NFS on PC</summary>

```shell
sudo apt install nfs-kernel-server
```

</details>

<details open>
<summary>Usage</summary>

```shell
sudo vi /etc/exports
```

After entering edit mode, add the following rule:

```shell
# The following path is where it is shared to the board.
/home/sean/Desktop/realtek/mnt *(rw,no_root_squash,no_subtree_check,sync)
```

After saving the rule, you should use the following command to update the settings:

```shell
sudo exportfs -r
```

</details>

## <div align="center">Reaktek Board</div>

<div align="center" style="font-size: 18px; font-weight: bold;">Wiring</div>

<div align="center">
    <img src="../img/realtek_board.png" width="700">
</div>

<details open>
<summary>Power on the board</summary>

After connecting USB to TTL chip with Board and PC, enter minicom with proper settings. When you power on the board, you will see the message appear in your minicom terminal on PC.

<div align="center" style="font-size: 18px; font-weight: bold;">Received Message When Power ON</div>

<div align="center">
    <img src="../img/realtek_power_on.png" width="700">
</div>

</details>

<details open>
<summary>Set up NFS</summary>

When you enter the shell as shown below, you can press the Enter button to interact with the board.

<div align="center" style="font-size: 18px; font-weight: bold;">Interact with Board</div>

<div align="center">
    <img src="../img/enter_board.png" width="700">
</div>

In the next step, we will first set the IP and then use the "mount" command to link the computer's specific path (Define in the /etc/exports) to the local position on the board.

```shell
ifconfig eth0 192.168.XXX.XXX
```

<div align="center">
    <img src="../img/ifconfig.png" width="700">
</div>

Ensure both sides are on the same IP subnet (set Ethernet as Static IP on PC); otherwise, the following step will fail. You can try "ping" command to check connection status.

```shell
mount -t nfs -o nolock 192.168.XXX.XXX:/path/to/your/folder/ /mnt/
```

<!-- ![alt text](image.png) -->

<div align="center">
    <img src="../img/mount.png" width="700">
</div>

</details>

Congratulations! You have completed this tutorial. You can refer to other documents below:

- [How To Transfer Model](../doc/transfer.md)
