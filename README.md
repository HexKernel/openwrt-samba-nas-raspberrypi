**Guide to Turning a Raspberry Pi Running OpenWrt into a Samba-Based NAS**



This repository serves as a practical guide for repurposing a Raspberry Pi running OpenWrt into a network-accessible file storage system by utilizing the storage resources available to the device. The core aim is to make data stored on the SD card or on any additional storage media connected to the Raspberry Pi accessible to other machines within the local network through the Samba (SMB/CIFS) file sharing protocol. 

Rather than being limited to a dedicated data partition, the shared storage can take the form of a specific directory within the existing OpenWrt filesystem or reside on external media such as USB drives or external hard disks attached to the device. 

The initial focus is on accurately detecting the target storage device, selecting an appropriate filesystem location, and mounting it persistently within OpenWrt. Particular attention is given to ensuring that mounts survive system reboots and that file permissions and ownership are correctly configured for network access. Once the storage layer is established, the repository details the setup and configuration of Samba on OpenWrt, including share definitions, access control, and basic security considerations. Through this approach, the Raspberry Pi is converted into a compact, low-overhead file server capable of providing centralized storage services across a LAN, suitable for home networks, experimental environments, or embedded deployments.


> ⚠️ **Note**
> 
> Please note that due to the way Samba handles file transfers, RAM consumption in the form of filesystem cache will occur while files are being transferred from other network-connected devices to the defined shared storage. During an active transfer, data is buffered in RAM and the cache may grow as needed, potentially up to the size of the file being written. Once the transfer completes successfully, this cached memory is released automatically. However, if the file being transferred is larger than the available RAM allocated for caching, the transfer may be interrupted once the maximum usable cache limit is reached. In such cases, the cached data can remain in memory, effectively saturating available RAM, until it is cleared by the system’s automatic cache reclamation mechanisms or by a **manual cache flush**.
