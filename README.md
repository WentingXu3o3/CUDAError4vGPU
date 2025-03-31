# CUDAError4vGPU
This is a sharing post for CUDA Error for vGPU env.


## Error Description:
* "nvidia-smi" works well
* python3 "import torch; torch.zeros(2,3).to("cuda")" shows error:
```
Python 3.8.10 (default, Mar 18 2025, 20:04:55) 
[GCC 9.4.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> import torch
>>> torch.zeros(2,3).to("cuda")
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
RuntimeError: CUDA error: operation not supported
CUDA kernel errors might be asynchronously reported at some other API call, so the stacktrace below might be incorrect.
For debugging consider passing CUDA_LAUNCH_BLOCKING=1
Compile with `TORCH_USE_CUDA_DSA` to enable device-side assertions.
```
* This error could be fixed by reinstall the nvidia-gpu driver, but it would be back in the several days



## Possible Solution:
* By regarding https://github.com/pytorch/pytorch/issues/135126, it could be related to the vGPU
* "nvidia-smi -q" and you can find my info indicating my machine is with vGPU while the physical one is Nvidia-A6000
* and check vGPU user guide with https://docs.nvidia.com/vgpu/13.0/grid-vgpu-user-guide/index.html#cuda-open-cl-support-vgpu
* We can find the vGPU license "unlicensed" here.
  try to figure it out with:
  https://docs.nvidia.com/vgpu/13.0/grid-vgpu-user-guide/index.html#licensing-grid-vgpu
```
  ==============NVSMI LOG==============

Timestamp                                 : Mon Mar 31 05:01:08 2025
Driver Version                            : 535.183.06
CUDA Version                              : 12.2

Attached GPUs                             : 1
GPU 00000000:00:10.0
    Product Name                          : NVIDIA RTXA6000-24Q
    Product Brand                         : NVIDIA RTX Virtual Workstation
    Product Architecture                  : Ampere
    Display Mode                          : Enabled
    Display Active                        : Disabled
    Persistence Mode                      : Enabled
    Addressing Mode                       : None
    MIG Mode
        Current                           : Disabled
        Pending                           : Disabled
    Accounting Mode                       : Disabled
    Accounting Mode Buffer Size           : 4000
    Driver Model
        Current                           : N/A
        Pending                           : N/A
    Serial Number                         : N/A
    GPU UUID                              : GPU-bf0881b6-032a-11f0-825b-5c07a73a413d
    Minor Number                          : 0
    VBIOS Version                         : 00.00.00.00.00
    MultiGPU Board                        : No
    Board ID                              : 0x10
    Board Part Number                     : N/A
    GPU Part Number                       : 2230-875-A1
    FRU Part Number                       : N/A
    Module ID                             : N/A
    Inforom Version
        Image Version                     : N/A
        OEM Object                        : N/A
        ECC Object                        : N/A
        Power Management Object           : N/A
    Inforom BBX Object Flush
        Latest Timestamp                  : N/A
        Latest Duration                   : N/A
    GPU Operation Mode
        Current                           : N/A
        Pending                           : N/A
    GSP Firmware Version                  : N/A
    GPU Virtualization Mode
        Virtualization Mode               : VGPU
        Host VGPU Mode                    : N/A
    vGPU Software Licensed Product
        Product Name                      : NVIDIA RTX Virtual Workstation
        License Status                    : Unlicensed
    GPU Reset Status
        Reset Required                    : N/A
        Drain and Reset Recommended       : N/A
    IBMNPU
        Relaxed Ordering Mode             : N/A
    PCI
        Bus                               : 0x00
        Device                            : 0x10
        Domain                            : 0x0000
        Device Id                         : 0x223010DE
        Bus Id                            : 00000000:00:10.0
        Sub System Id                     : 0x150410DE
        GPU Link Info
            PCIe Generation
                Max                       : N/A
                Current                   : N/A
                Device Current            : N/A
                Device Max                : N/A
                Host Max                  : N/A
            Link Width
                Max                       : N/A
                Current                   : N/A
        Bridge Chip
            Type                          : N/A
            Firmware                      : N/A
        Replays Since Reset               : N/A
        Replay Number Rollovers           : N/A
        Tx Throughput                     : N/A
        Rx Throughput                     : N/A
        Atomic Caps Inbound               : N/A
        Atomic Caps Outbound              : N/A
    Fan Speed                             : N/A
    Performance State                     : P8
    Clocks Event Reasons                  : N/A
    Sparse Operation Mode                 : N/A
    FB Memory Usage
        Total                             : 24576 MiB
        Reserved                          : 2134 MiB
        Used                              : 47 MiB
        Free                              : 22394 MiB
    BAR1 Memory Usage
        Total                             : 256 MiB
        Used                              : 0 MiB
        Free                              : 256 MiB
    Conf Compute Protected Memory Usage
        Total                             : 0 MiB
        Used                              : 0 MiB
        Free                              : 0 MiB
    Compute Mode                          : Default
    Utilization
        Gpu                               : 0 %
        Memory                            : 0 %
        Encoder                           : 0 %
        Decoder                           : 0 %
        JPEG                              : N/A
        OFA                               : N/A
    Encoder Stats
        Active Sessions                   : 0
        Average FPS                       : 0
        Average Latency                   : 0
    FBC Stats
        Active Sessions                   : 0
        Average FPS                       : 0
        Average Latency                   : 0
    ECC Mode
        Current                           : Enabled
        Pending                           : Enabled
    ECC Errors
        Volatile
            SRAM Correctable              : N/A
            SRAM Uncorrectable Parity     : N/A
            SRAM Uncorrectable SEC-DED    : N/A
            DRAM Correctable              : 0
            DRAM Uncorrectable            : 0
        Aggregate
            SRAM Correctable              : N/A
            SRAM Uncorrectable Parity     : N/A
            SRAM Uncorrectable SEC-DED    : N/A
            DRAM Correctable              : 0
            DRAM Uncorrectable            : 0
            SRAM Threshold Exceeded       : N/A
        Aggregate Uncorrectable SRAM Sources
            SRAM L2                       : N/A
            SRAM SM                       : N/A
            SRAM Microcontroller          : N/A
            SRAM PCIE                     : N/A
            SRAM Other                    : N/A
    Retired Pages
        Single Bit ECC                    : N/A
        Double Bit ECC                    : N/A
        Pending Page Blacklist            : N/A
    Remapped Rows                         : N/A
    Temperature
        GPU Current Temp                  : N/A
        GPU T.Limit Temp                  : N/A
        GPU Shutdown Temp                 : N/A
        GPU Slowdown Temp                 : N/A
        GPU Max Operating Temp            : N/A
        GPU Target Temperature            : N/A
        Memory Current Temp               : N/A
        Memory Max Operating Temp         : N/A
    GPU Power Readings
        Power Draw                        : N/A
        Current Power Limit               : N/A
        Requested Power Limit             : N/A
        Default Power Limit               : N/A
        Min Power Limit                   : N/A
        Max Power Limit                   : N/A
    Module Power Readings
        Power Draw                        : N/A
        Current Power Limit               : N/A
        Requested Power Limit             : N/A
        Default Power Limit               : N/A
        Min Power Limit                   : N/A
        Max Power Limit                   : N/A
    Clocks
        Graphics                          : 210 MHz
        SM                                : 210 MHz
        Memory                            : 405 MHz
        Video                             : 555 MHz
    Applications Clocks
        Graphics                          : N/A
        Memory                            : N/A
    Default Applications Clocks
        Graphics                          : N/A
        Memory                            : N/A
    Deferred Clocks
        Memory                            : N/A
    Max Clocks
        Graphics                          : N/A
        SM                                : N/A
        Memory                            : N/A
        Video                             : N/A
    Max Customer Boost Clocks
        Graphics                          : N/A
    Clock Policy
        Auto Boost                        : N/A
        Auto Boost Default                : N/A
    Voltage
        Graphics                          : N/A
    Fabric
        State                             : N/A
        Status                            : N/A
    Processes
        GPU instance ID                   : N/A
        Compute instance ID               : N/A
        Process ID                        : 1117
            Type                          : G
            Name                          : /usr/lib/xorg/Xorg
            Used GPU Memory               : 23 MiB
        GPU instance ID                   : N/A
        Compute instance ID               : N/A
        Process ID                        : 1717
            Type                          : G
            Name                          : /usr/lib/xorg/Xorg
            Used GPU Memory               : 23 MiB

  ```
* Follow the instructions for license configuration and change&save the file
```
carlab@carlab:~$ sudo cat /etc/nvidia/ClientConfigToken/gridd.conf
# /etc/nvidia/gridd.conf.template - Configuration file for NVIDIA Grid Daemon
…
# Description: Set Feature to be enabled
# Data type: integer
# Possible values:
# 0 => for unlicensed state
# 1 => for NVIDIA vGPU
# 2 => for NVIDIA RTX Virtual Workstation
# 4 => for NVIDIA Virtual Compute Server
FeatureType=2
```
*after reinstall the nvida-driver, and reboot
get
```
carlab@carlab:~$ nvidia-smi -q

==============NVSMI LOG==============

Timestamp                                 : Mon Mar 31 06:56:42 2025
Driver Version                            : 535.183.06
CUDA Version                              : 12.2

Attached GPUs                             : 1
GPU 00000000:00:10.0
    Product Name                          : NVIDIA RTXA6000-24Q
    Product Brand                         : NVIDIA RTX Virtual Workstation
    Product Architecture                  : Ampere
    Display Mode                          : Enabled
    Display Active                        : Disabled
    Persistence Mode                      : Disabled
    Addressing Mode                       : None
    MIG Mode
        Current                           : Disabled
        Pending                           : Disabled
    Accounting Mode                       : Disabled
    Accounting Mode Buffer Size           : 4000
    Driver Model
        Current                           : N/A
        Pending                           : N/A
    Serial Number                         : N/A
    GPU UUID                              : GPU-bf0881b6-032a-11f0-825b-5c07a73a413d
    Minor Number                          : 0
    VBIOS Version                         : 00.00.00.00.00
    MultiGPU Board                        : No
    Board ID                              : 0x10
    Board Part Number                     : N/A
    GPU Part Number                       : 2230-875-A1
    FRU Part Number                       : N/A
    Module ID                             : N/A
    Inforom Version
        Image Version                     : N/A
        OEM Object                        : N/A
        ECC Object                        : N/A
        Power Management Object           : N/A
    Inforom BBX Object Flush
        Latest Timestamp                  : N/A
        Latest Duration                   : N/A
    GPU Operation Mode
        Current                           : N/A
        Pending                           : N/A
    GSP Firmware Version                  : N/A
    GPU Virtualization Mode
        Virtualization Mode               : VGPU
        Host VGPU Mode                    : N/A
    vGPU Software Licensed Product
        Product Name                      : NVIDIA RTX Virtual Workstation
        License Status                    : Unlicensed (Unrestricted)
    GPU Reset Status
        Reset Required                    : N/A
        Drain and Reset Recommended       : N/A
    IBMNPU
        Relaxed Ordering Mode             : N/A
    PCI
        Bus                               : 0x00
        Device                            : 0x10
        Domain                            : 0x0000
        Device Id                         : 0x223010DE
        Bus Id                            : 00000000:00:10.0
        Sub System Id                     : 0x150410DE
        GPU Link Info
            PCIe Generation
                Max                       : N/A
                Current                   : N/A
                Device Current            : N/A
                Device Max                : N/A
                Host Max                  : N/A
            Link Width
                Max                       : N/A
                Current                   : N/A
        Bridge Chip
            Type                          : N/A
            Firmware                      : N/A
        Replays Since Reset               : N/A
        Replay Number Rollovers           : N/A
        Tx Throughput                     : N/A
        Rx Throughput                     : N/A
        Atomic Caps Inbound               : N/A
        Atomic Caps Outbound              : N/A
    Fan Speed                             : N/A
    Performance State                     : P8
    Clocks Event Reasons                  : N/A
    Sparse Operation Mode                 : N/A
    FB Memory Usage
        Total                             : 24576 MiB
        Reserved                          : 2134 MiB
        Used                              : 47 MiB
        Free                              : 22394 MiB
    BAR1 Memory Usage
        Total                             : 256 MiB
        Used                              : 0 MiB
        Free                              : 256 MiB
    Conf Compute Protected Memory Usage
        Total                             : 0 MiB
        Used                              : 0 MiB
        Free                              : 0 MiB
    Compute Mode                          : Default
    Utilization
        Gpu                               : 0 %
        Memory                            : 0 %
        Encoder                           : 0 %
        Decoder                           : 0 %
        JPEG                              : N/A
        OFA                               : N/A
    Encoder Stats
        Active Sessions                   : 0
        Average FPS                       : 0
        Average Latency                   : 0
    FBC Stats
        Active Sessions                   : 0
        Average FPS                       : 0
        Average Latency                   : 0
    ECC Mode
        Current                           : Enabled
        Pending                           : Enabled
    ECC Errors
        Volatile
            SRAM Correctable              : N/A
            SRAM Uncorrectable Parity     : N/A
            SRAM Uncorrectable SEC-DED    : N/A
            DRAM Correctable              : 0
            DRAM Uncorrectable            : 0
        Aggregate
            SRAM Correctable              : N/A
            SRAM Uncorrectable Parity     : N/A
            SRAM Uncorrectable SEC-DED    : N/A
            DRAM Correctable              : 0
            DRAM Uncorrectable            : 0
            SRAM Threshold Exceeded       : N/A
        Aggregate Uncorrectable SRAM Sources
            SRAM L2                       : N/A
            SRAM SM                       : N/A
            SRAM Microcontroller          : N/A
            SRAM PCIE                     : N/A
            SRAM Other                    : N/A
    Retired Pages
        Single Bit ECC                    : N/A
        Double Bit ECC                    : N/A
        Pending Page Blacklist            : N/A
    Remapped Rows                         : N/A
    Temperature
        GPU Current Temp                  : N/A
        GPU T.Limit Temp                  : N/A
        GPU Shutdown Temp                 : N/A
        GPU Slowdown Temp                 : N/A
        GPU Max Operating Temp            : N/A
        GPU Target Temperature            : N/A
        Memory Current Temp               : N/A
        Memory Max Operating Temp         : N/A
    GPU Power Readings
        Power Draw                        : N/A
        Current Power Limit               : N/A
        Requested Power Limit             : N/A
        Default Power Limit               : N/A
        Min Power Limit                   : N/A
        Max Power Limit                   : N/A
    Module Power Readings
        Power Draw                        : N/A
        Current Power Limit               : N/A
        Requested Power Limit             : N/A
        Default Power Limit               : N/A
        Min Power Limit                   : N/A
        Max Power Limit                   : N/A
    Clocks
        Graphics                          : 210 MHz
        SM                                : 210 MHz
        Memory                            : 405 MHz
        Video                             : 555 MHz
    Applications Clocks
        Graphics                          : N/A
        Memory                            : N/A
    Default Applications Clocks
        Graphics                          : N/A
        Memory                            : N/A
    Deferred Clocks
        Memory                            : N/A
    Max Clocks
        Graphics                          : N/A
        SM                                : N/A
        Memory                            : N/A
        Video                             : N/A
    Max Customer Boost Clocks
        Graphics                          : N/A
    Clock Policy
        Auto Boost                        : N/A
        Auto Boost Default                : N/A
    Voltage
        Graphics                          : N/A
    Fabric
        State                             : N/A
        Status                            : N/A
    Processes
        GPU instance ID                   : N/A
        Compute instance ID               : N/A
        Process ID                        : 1144
            Type                          : G
            Name                          : /usr/lib/xorg/Xorg
            Used GPU Memory               : 23 MiB
        GPU instance ID                   : N/A
        Compute instance ID               : N/A
        Process ID                        : 1636
            Type                          : G
            Name                          : /usr/lib/xorg/Xorg
            Used GPU Memory               : 23 MiB
```
But
```
carlab@carlab:~$ sudo systemctl status nvidia-gridd
[sudo] password for carlab: 
● nvidia-gridd.service - NVIDIA Grid Daemon
     Loaded: loaded (/lib/systemd/system/nvidia-gridd.service; enabled; vendor preset: enabled)
     Active: failed (Result: exit-code) since Mon 2025-03-31 06:53:50 UTC; 7min ago
    Process: 1030 ExecStart=/usr/bin/nvidia-gridd (code=exited, status=0/SUCCESS)
    Process: 1113 ExecStopPost=/bin/rm -rf /var/run/nvidia-gridd (code=exited, status=0/SUCCESS)
   Main PID: 1039 (code=exited, status=1/FAILURE)

Mar 31 06:53:49 carlab systemd[1]: Started NVIDIA Grid Daemon.
Mar 31 06:53:50 carlab nvidia-gridd[1039]: vGPU Software package (0)
Mar 31 06:53:50 carlab nvidia-gridd[1039]: Ignore service provider and node-locked licensing
Mar 31 06:53:50 carlab nvidia-gridd[1039]: NLS initialized
Mar 31 06:53:50 carlab nvidia-gridd[1039]: Failed to decode signature from token received
Mar 31 06:53:50 carlab nvidia-gridd[1039]: Failed to read configurations from client configuration token (Error: >
Mar 31 06:53:50 carlab nvidia-gridd[1039]: Failed to setup cloud License Manager: 3
Mar 31 06:53:50 carlab nvidia-gridd[1039]: Shutdown (1039)
Mar 31 06:53:50 carlab systemd[1]: nvidia-gridd.service: Main process exited, code=exited, status=1/FAILURE
Mar 31 06:53:50 carlab systemd[1]: nvidia-gridd.service: Failed with result 'exit-code'.
lines 1-17/17 (END)

```
![Screenshot 2025-03-31 at 17 01 02](https://github.com/user-attachments/assets/becb48a7-8d50-4c16-b4c0-0a12a56ea99c)
