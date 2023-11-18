# 8311 WAS-110 Firmware Builder

## custom fwenvs
```
8311_fix_vlans=1
8311_internet_vlan=0
8311_services_vlan=36

8311_ipaddr=192.168.11.1
8311_netmask=255.255.255.0
8311_gateway=192.168.11.254
8311_ping_ip=192.168.11.2

8311_console_en=1
8311_ethtool_speed=speed 2500 autoneg off duplex full
8311_failsafe_delay=30
8311_persist_root=0
8311_root_pwhash=$1$BghTQV7M$ZhWWiCgQptC1hpUdIfa0e.
8311_rx_los=0

8311_cp_hw_ver_sync=1
8311_device_sn=DM222XXXXXXXXXX
8311_equipment_id=5690
8311_gpon_sn=SMBSXXXXXXXX
8311_hw_ver=Fast5689EBell
8311_mib_file=/etc/mibs/prx300_1V.ini
8311_reg_id_hex=00
8311_sw_verA=SGC830007C
8311_sw_verB=SGC830006E
8311_vendor_id=SMBS
```


### 8311_cp_hw_ver_sync
**Sync Circuit Pack with Hardware Version**
When set to `1` and `8311_hw_ver` is also set, will modify the configured mib file to set the Version field of any Circuit Pack MEs to match the Hardware version

### 8311_device_sn
**Device Serial Number**
Sets the physical device S/N, this is more or less display only

### 8311_equipment_id
**Equipment ID**
Sets the PON Equipment ID field in the ONU2-G ME (257)

### 8311_gpon_sn
**GPON Serial Number**
Sets the GPON Serial Number sent to the OLT in various MEs (4 letters, followed by 8 hex digits)

### 8311_hw_ver
**Hardware Version**
Set the Hardware version string sent to the OLT in various MEs (up to 14 characters)

### 8311_mib_file
**MIB File**
Sets the MIB file used by omcid. Defaults to `/etc/mibs/prx300_1U.ini`

### 8311_reg_id_hex
**Registration ID**
Sets the Registration ID sent to the OLT in hex format

### 8311_sw_ver / 8311_sw_verA / 8311_sw_verB
**Software Version**
Sets the default and/or image specific software versions sent in the Software image MEs (7)

### 8311_vendor_id
**Vendor ID**
Sets the PON Vendor ID sent to the OLT, automatically derived from the GPON Serial Number if not set (4 letters)


## custom uci settings
`uci -qc /ptconf/8311 show`  
```
dropbear.rsa_key=key
dropbear.rsa_key.value='BASE64 of the RSA server key'
dropbear.public_key=key
dropbear.public_key.value='ssh-rsa public key' 
```

## Scripts

### build.sh
Tool for building new modded WAS-110 firmware images
```
Usage: ./build.sh [options]

Options:
-i --image <filename>           Specify stock local upgrade image file.
-I --image-dir <dir>            Specify stock image directory (must contain bootcore.bin, kernel.bin, and rootfs.img).
-o --image-out <filename>       Specify local upgrade image to output.
-h --help                       This help text
```

### create.sh
Tool for creating new WAS-110 local upgrade images
```
Usage: ./create.sh [options]

Options:
-i --image <filename>           Specify local upgrade image file to create (required).
-H --header <filename>          Specify filename of image header to base image off of (default: header.bin).
-b --bootcore <filename>        Specify filename of bootcore image to place in created image (default: bootcore.bin).
-k --kernel <filename>          Specify filename of kernel image to place in created image (default: kernel.bin).
-r --rootfs <filename>          Specify filename of rootfs image to place in created image (default: rootfs.img).
-V --image-version <version>    Specify version string to set on created image (14 characters max).
-h --help                       This help text
```


### extract.sh
Tool for extracting stock WAS-110 local upgrade images
```
Usage: ./extract.sh [options]

Options:
-i --image <filename>           Specify local upgrade image file to extract (required).
-H --header <filename>          Specify filename to extract image header to (default: header.bin).
-b --bootcore <filename>        Specify filename to extract bootcore image to (default: bootcore.bin).
-k --kernel <filename>          Specify filename to extract kernel image to (default: kernel.bin).
-r --rootfs <filename>          Specify filename to extract rootfs image to (default: rootfs.img).
-h --help                       This help text
```
