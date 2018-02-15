---
layout: post
summary: "VeraCrypt, a wonderful cross-platform encryption software"
tags: tech security
---
https://veracrypt.codeplex.com/

### What does VeraCrypt bring to you?

- VeraCrypt adds enhanced security to the algorithms used for system and partitions encryption making it immune to new developments in brute-force attacks.
- VeraCrypt also solves many vulnerabilities and security issues found in TrueCrypt. The following post describes some of the enhancements and corrections done: https://veracrypt.codeplex.com/discussions/569777#PostContent_1313325
- As an example, when the system partition is encrypted, TrueCrypt uses PBKDF2-RIPEMD160 with 1000 iterations whereas in VeraCrypt we use 327661. And for standard containers and other partitions, TrueCrypt uses at most 2000 iterations but VeraCrypt uses 655331 for RIPEMD160 and 500000 iterations for SHA-2 and Whirlpool.
- This enhanced security adds some delay only to the opening of encrypted partitions without any performance impact to the application use phase. This is acceptable to the legitimate owner but it makes it much harder for an attacker to gain access to the encrypted data.
- Cross platform: Windows - MacOS - Linux

### How can I use VeraCrypt on a USB flash drive?

You have three options:

1. Encrypt the entire USB flash drive. However, you will not be able run VeraCrypt from the USB flash drive.

2. Create two or more partitions on your USB flash drive. Leave the first partition non encrypted and encrypt the other partition(s). You can store VeraCrypt on the first partition in order to run it directly from the USB flash drive.
> Note: Windows can only access the primary partition of a USB flash drive, nevertheless the extra partitions remain accessible through VeraCrypt.

3. Create a VeraCrypt file container on the USB flash drive (for information on how to do so, see the chapter [Beginner's Tutorial](https://veracrypt.codeplex.com/wikipage?title=Beginner%27s%20Tutorial), in the [VeraCrypt User Guide](https://veracrypt.codeplex.com/documentation)). If you leave enough space on the USB flash drive (choose an appropriate size for the VeraCrypt container), you will also be able to store VeraCrypt on the USB flash drive (along with the container – not in the container) and you will be able to run VeraCrypt from the USB flash drive (see also the chapter [Portable Mode](https://veracrypt.codeplex.com/wikipage?title=Portable%20Mode) in the VeraCrypt User Guide).
