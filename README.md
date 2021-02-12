# Installation eines Multioboot PXE Servers mit Syslinux (UEFI/BIOS)

### 1. Pakete Installieren
```shell
apt install syslinux-common syslinux-efi tftp-hpa unzip -y
```

### 2. Erstellen des  tftp-root
```shell
mkdir /tftpboot
```
### 3. PXE und Syslinux Dateien

##### BIOS (Empfolen)
```shell
cd /tftpboot
wget URL
unzip *.zip

```

##### UEFI
```shell
cd /tftpboot
wget URL
unzip *.zip
```
### 4. Konfiguration von tftpd-hpa
```shell
nano /etc/default/tftpd-hpa
```
```text
TFTP_USERNAME="tftp"
TFTP_DIRECTORY="/tftpboot"
TFTP_ADDRESS="0.0.0.0:69"
TFTP_OPTIONS="--secure"
```
```shell
systemctl restart tftpd-hpa.service
```
### 5. Eintrag im Router Vornehmen und Images Downloaden

##### Roter Eintrag Gemäß "gateway.conf"
```text
#####################################################################################################
#Damit die Clients via DHCP den PXE Server "Sehen" können müssen wir per am Router darauf verweisen!#
#Dies Geschieht über die Boot Datei die je nach UEFI oder BIOS Boot im DHCP Server hinterlegt wird. #
#####################################################################################################
UEFI = PXE via TFTP = syslinux.efi
BIOS = PXE via TFTP = pxelinux.0
```
##### Fertige PXE Images:

- [Debian](https://www.debian.org/CD/netinst/)
- [Von mir zur verfügung gestellte Utils](URL)

