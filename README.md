# 🛡️ Building My First Cybersecurity Lab — Kali Linux on VirtualBox

![Platform](https://img.shields.io/badge/Platform-Windows-blue?style=for-the-badge&logo=windows)
![Virtualization](https://img.shields.io/badge/Virtualization-VirtualBox-183A61?style=for-the-badge&logo=virtualbox)
![Operating System](https://img.shields.io/badge/OS-Kali%20Linux-557C94?style=for-the-badge&logo=kalilinux)
![Status](https://img.shields.io/badge/Status-Active%20Learning-success?style=for-the-badge)

## 📌 About This Project

Welcome to my first hands-on cybersecurity lab!

As a Computer Science student, I wanted to move beyond reading about cybersecurity and start gaining practical experience with Linux, networking, virtualization, and security tools.

I decided to build a personal lab by running **Kali Linux inside Oracle VirtualBox on a Windows laptop**. This approach lets me explore a Linux environment while keeping Windows available for my everyday work and studies.

The setup was not completely straightforward. I encountered boot errors, virtual machine registration conflicts, storage limitations, and questions about network configuration. Working through these challenges helped me understand that cybersecurity involves more than using tools — it also requires troubleshooting, patience, and understanding how systems work.

This repository documents my setup process, the problems I encountered, the solutions that helped, and my next steps toward becoming more skilled in cybersecurity.

> My goal is to build a strong foundation in Linux, computer networking, ethical hacking, and defensive security through consistent hands-on practice.

---

## 🎯 Project Objectives

- Install and run Kali Linux in a virtualized environment.
- Understand the basics of virtualization and virtual hard disks.
- Configure virtual machine memory and storage settings.
- Investigate boot problems and virtual machine errors.
- Explore network connectivity in Kali Linux.
- Create a shared folder between Windows and Kali Linux.
- Transfer files between the host and guest operating systems.
- Develop confidence using the Linux terminal.
- Prepare a safe environment for future cybersecurity exercises.

---

## 🧰 Tools and Technologies

| Tool | Purpose |
|---|---|
| Windows | Host operating system |
| Oracle VirtualBox | Runs Kali Linux as a virtual machine |
| Kali Linux | Linux distribution designed for security testing and related tasks |
| 7-Zip | Extracts the downloaded virtual machine archive |
| VirtualBox Shared Folders | Transfers files between Windows and Kali Linux |
| Linux Terminal | Runs commands and performs system administration tasks |
| GitHub | Documents my learning journey and project progress |

### 💻 Lab Environment

- **Host operating system:** Windows
- **Guest operating system:** Kali Linux
- **Virtualization platform:** Oracle VirtualBox
- **Laptop storage:** 64 GB
- **Virtual machine memory allocation:** Approximately 2 GB RAM
- **File-sharing directory:** `/media/sf_KaliShare`

*Note: These are the settings used during my setup. Actual available memory and storage can vary.*

---

# 🚀 My Setup Journey

## 1. Downloading Kali Linux

I began by downloading the prebuilt Kali Linux image designed for VirtualBox.

Using a prebuilt virtual machine image meant I did not need to create a new virtual hard disk and install Kali manually from an ISO image.

Official download page: https://www.kali.org/get-kali/

I selected the VirtualBox image, downloaded the archive, and prepared it for extraction.

## 2. Extracting the Virtual Machine

After downloading Kali Linux, I used 7-Zip to extract the archive.

The important files included:

- `.vbox` — contains the virtual machine configuration.
- `.vdi` — represents the virtual hard disk containing the guest operating system and its data.

I learned that these files serve different purposes. The configuration file defines the virtual machine, while the virtual disk stores its operating system and files.

**Key lesson:** A downloaded archive must extract successfully before the virtual machine can be expected to work correctly.

## 3. Importing Kali Linux into VirtualBox

I opened the extracted `.vbox` file to register Kali Linux in VirtualBox.

During this process, VirtualBox reported a machine UUID conflict because a machine with the same unique identifier was already registered.

I learned that VirtualBox tracks registered virtual machines using unique identifiers and that removing a registration is different from deleting the virtual machine's files.

This was an important lesson in managing virtual machines safely.

## 4. Troubleshooting the `grub rescue>` Error

One of the main challenges I encountered was the following boot error:

```text
grub rescue>
```

This indicated that the bootloader could not locate the files it needed to continue starting the operating system.

I investigated several possible causes, including:

- Virtual machine registration.
- Virtual disk attachment.
- Storage configuration.
- UEFI and motherboard settings.
- File extraction and storage limitations.

I also learned to inspect VirtualBox's storage settings and confirm whether the virtual disk was attached to the virtual machine.

This experience showed me the importance of checking the boot process systematically rather than changing random settings.

## 5. Configuring Virtual Machine Resources

My laptop has limited storage and memory, so resource allocation was an important consideration.

I checked the virtual machine's memory settings and used an allocation of approximately 2 GB RAM.

VirtualBox also displayed a warning about assigning too much memory to the guest system.

This taught me that a virtual machine shares physical resources with the host operating system. Allocating too much RAM or disk space can affect Windows performance.

**Lesson learned:** Virtual machines should be configured according to the host computer's available resources.

## 6. Working With Limited Storage

My laptop has a 64 GB drive, which made storage management challenging.

I checked the storage usage in Windows, reviewed installed applications, and used Windows storage tools to identify files that could be removed safely.

I also learned not to delete important system directories such as `C:\Windows` or `C:\Program Files` manually.

This part of the project reinforced the importance of protecting system files and maintaining sufficient free space when working with virtual machines.

## 7. Exploring Network Configuration

After getting into Kali Linux, I began working on its network configuration.

Networking is essential in cybersecurity because systems communicate through network interfaces, IP addresses, ports, and protocols.

My next learning goals in this area include:

- Understanding virtual network adapters.
- Learning the difference between NAT and bridged networking.
- Checking network interface status.
- Testing connectivity.
- Understanding IP addressing and DNS resolution.

These concepts will provide the foundation needed for later networking and security exercises.

## 8. Creating a Shared Folder Between Windows and Kali Linux

One of the most useful features I configured was VirtualBox Shared Folders.

My goal was to access files stored in Kali Linux from Windows and transfer files without repeatedly using a flash drive.

### Step 1: Create a folder in Windows

I created a folder named:

```text
KaliShare
```

This folder acts as the shared location between the two operating systems.

### Step 2: Configure VirtualBox

I opened the Kali Linux virtual machine settings and navigated to:

```text
Settings → Shared Folders
```

I added the Windows folder and enabled:

- Auto-mount
- Make Permanent

This allowed the shared folder configuration to remain available across virtual machine restarts.

### Step 3: Configure user permissions

I used the following Linux command to add my current user to the VirtualBox shared-folder group:

```bash
sudo usermod -aG vboxsf "$USER"
```

I then restarted Kali Linux:

```bash
sudo reboot
```

The `vboxsf` group provides access to VirtualBox shared folders when the required Guest Additions components are installed and working.

### Step 4: Access the shared directory

The shared folder became accessible at:

```text
/media/sf_KaliShare
```

I could check its contents with:

```bash
ls /media/sf_KaliShare
```

### Step 5: Transfer files

For example, I could copy a file from my Downloads directory into the shared folder:

```bash
cp ~/Downloads/example.txt /media/sf_KaliShare/
```

After copying the file, I could access it from the corresponding `KaliShare` folder in Windows.

**Result:** I successfully configured a shared folder and used it to transfer files between Kali Linux and Windows.

---

# 🧠 Important Concepts I Learned

### Virtualization

Virtualization allows one physical computer to run another operating system inside a virtual machine.

### Virtual hard disks

A `.vdi` file acts as a virtual disk for VirtualBox. Its file size on Windows can be smaller than its maximum virtual capacity, particularly when dynamically allocated.

### Bootloaders

GRUB helps load Linux during startup. A `grub rescue>` prompt indicates a boot problem that requires investigation.

### Linux permissions

Linux uses users, groups, and permissions to control access to files and system resources.

### Networking

Virtual machines use virtual network adapters to communicate with other systems and, depending on configuration, external networks.

### Shared folders

Shared folders provide a convenient way to exchange files between a host operating system and a guest virtual machine.

---

# 🔐 Security and Ethical Practice

My goal is to learn cybersecurity responsibly.

All future testing will be performed on systems I own, intentionally vulnerable training environments, or systems for which I have explicit authorization.

I intend to focus on understanding vulnerabilities, learning how to detect security problems, and developing defensive skills alongside practical testing.

---

# 📚 My Next Learning Roadmap

- [ ] Learn essential Linux terminal commands.
- [ ] Understand Linux users, groups, and file permissions.
- [ ] Study TCP/IP, DNS, ports, and network interfaces.
- [ ] Practise network troubleshooting.
- [ ] Learn Wireshark for network traffic analysis.
- [ ] Learn Nmap for authorized network discovery.
- [ ] Explore web application security in a training lab.
- [ ] Study common vulnerabilities and their mitigations.
- [ ] Document practical exercises and lessons learned.
- [ ] Build a small portfolio of cybersecurity projects.

---

# 🏁 Project Outcome

This project gave me practical experience setting up a Linux virtual machine and troubleshooting issues involving boot configuration, virtual disks, system resources, and file sharing.

The most useful outcome was learning how to exchange files between Windows and Kali Linux through a working shared folder.

I now have a foundation for continuing my cybersecurity studies and building more advanced lab exercises.

**Project status:** Initial lab setup and shared-folder configuration completed. Further networking and security exercises are planned.

---

## 👨‍💻 About Me

I am a Computer Science student developing practical skills in programming, Linux, networking, and cybersecurity.

I use projects like this to document what I learn, troubleshoot real technical problems, and build a portfolio of hands-on experience.

**This is the beginning of my cybersecurity journey — one lab, one challenge, and one lesson at a time.**

## 🔗 Useful Resources

- Kali Linux: https://www.kali.org/
- VirtualBox: https://www.virtualbox.org/
- GitHub Docs: https://docs.github.com/
- Wireshark: https://www.wireshark.org/
- Nmap: https://nmap.org/

---

*Disclaimer: This repository documents personal learning and lab configuration. It is not a claim of professional cybersecurity certification or expertise.*

