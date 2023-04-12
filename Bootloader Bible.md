- MOK - Machine Owner Keys
- ESP - EFI System Partition
- MBR - Master Boot Record

Secure Boot Key files:
https://sourceforge.net/p/refind/code/ci/master/tree/keys/
- copy files with .cer and .der extensions to the ESP 

https://www.freedesktop.org/wiki/Specifications/BootLoaderSpec/
https://en.altlinux.org/UEFI_SecureBoot_mini-HOWTO
https://wiki.ubuntu.com/UEFI/SecureBoot/Testing?action=show&redirect=SecurityTeam%2FSecureBoot

Managing EFI Boot Loaders for Linux:
http://www.rodsbooks.com/efi-bootloaders/index.html

Dealing with Secure Boot:
http://www.rodsbooks.com/efi-bootloaders/secureboot.html

Controling Secure Boot:
http://www.rodsbooks.com/efi-bootloaders/controlling-sb.html

# Self-signing:
#### Add generated public key to the MOK list

1. Generate a set of MOKs:
``$ openssl req -new -x509 -newkey rsa:2048 -keyout MOK.key -out MOK.crt \``
  ``-nodes -days 3650 -subj "/CN=Your Name/"``
``$ openssl x509 -in MOK.crt -out MOK.cer -outform DER``
- set "Your Name"
- set expiration date via the ``-days``

2. Copy the public key to the ESP

>Avoid Shim 0.1 doesn't support MOKs (Shipped with Ubuntu 12.10)
>In theory, any Shim from version 0.2 should work fine

3. Get the ``shim.efi`` or ``shimx64.efi`` from a distributions boot medium
4. Install ``MokManager`` should come with Shim, reside unter the name ``MokManager.efi`` or ``mmx64.efi``
5. Sign the follow-on boot loader as well as any unsigned kernel
6. Copy follow-on boot loader to the filename ``grubx64.efi`` in the same directory that holds ``shimx64.efi``

>If your Shim binary lacks the x64 filename component, chances are it will try to launch `grub.efi`
>Adjust filenames as necessary

7. Import MOKs using the ``mokutil`` program or copy the public keys that have .cer or .der filename extensions to the ESP

8. Reboot leads to the MokManager Shim launched when the boot loader failed verification
9. Press down arrow key and press Enter to select ``Enroll key from disk``
10. Select appropriate disk partition 
11. Navigate to the directory where the public keys copied to the ESP reside in
12. Select the public key file
13. Provide verification that you want to enroll the public key
14. Return to the MokManager main menu
15. Select ``Continue boot`` at the main menu

When the computer reboots it should boot the programm installed under the name ``grubx64.efi``

