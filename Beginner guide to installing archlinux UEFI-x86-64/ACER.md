## ACER laptop post-installation guide
If you have an ACER laptop, please perform the following extra steps:
AFTER installing Arch Linux and setting up the loader in the FAT32 EFI partition, the steps are: 

1- Get into BIOS - by pressing F2 when computer boots

2- Set Supervisor password 

3- Ensure Secure Boot is on

4- Go to "Select an UEFI file as trusted for execution" and choose: EFI - arch - grubx64.efi 

5- Turn off Secure Boot

6- In section 'Main', select F12 Boot Menu and change it to 'Enabled' 

7- Optionally, clear Supervisor password 

8- Save BIOS settings and restart

9- Press F12 on boot and now you can choose Arch.