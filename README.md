# leapp-upgrade-automation

## RHEL 7 --> RHEL 8 Upgrade Project

Repo containing all of the Ansible code used to execute an In-Place Upgrade (IPU) for RHEL 7 machines to RHEL 8 using the leapp package.

### Dependencies
- `ansible.posix`
- `community.general`
- `infra.leapp`
- `fedora.linux_system_roles`

### Supported Inhibitors

    - Title: Newest installed kernel not in use
      Summary: To ensure a stable upgrade, the machine needs to be booted into the latest installed kernel.
      Key: `ebba7acfa54d3fa3abc927ba510ebde9ed1d17`

    - Title: Multiple devel kernels installed
      Summary: DNF cannot produce a valid upgrade transaction when multiple kernel-devel packages are installed.
      Key: `8ceea8fa1bdb12329b7482ca721261509e5b256`

    - Title: Multiple debug kernels installed
      Summary: DNF cannot produce a valid upgrade transaction when multiple kernel-debug packages are installed.
      Key: `20dea2a6932622f6b8e9e12d13de0b85a3eb585`

    - Title: Detected incorrect order of entries or duplicate entries in /etc/fstab
      Summary: Leapp detected incorrect /etc/fstab format that causes overshadowing of mount points.
      Key: `fbb78588331fe656352ec13c2a1cb8e6a544fc`

    - Title: Use of NFS detected. Upgrade can't proceed
      Summary: NFS is currently not supported by the in-place upgrade.
      Key: `9881b25faceeeaa7a6478bcdac29afa7f5baaaed`

    - Title: Use of CIFS detected. Upgrade can't proceed
      Summary: CIFS is currently not supported by the in-place upgrade.
      Key: `de1aa3c7c4fca55ebdcbea2747ff46ad6af24`

    - Title: Btrfs has been removed from RHEL 8
      Summary: The Btrfs file system was introduced as Technology Preview with the initial release of Red Hat Enterprise Linux 6 and Red Hat Enterprise Linux 7. As of versions 6.6 and 7.4 this technology has been deprecated and removed in RHEL 8.
      Key: `196e2adc90782f4deb3cc0ce1367c7a8ad21f34`


    - Title: Upgrade requires links in root directory to be relative
      Summary: After rebooting, parts of the upgrade process can fail if symbolic links in / point to absolute paths.
      Key: `34895ad37cea4157b64d439ed6b6bd75562061f`

    - Title: Leapp detected loaded kernel drivers which have been removed in RHEL 8
      Summary: Support for the following RHEL 7 device drivers has been removed in RHEL 8:
    - `floppy`
    - `pata_acpi`
      Key: `e0820742002958de6af5c2699fae9ec2eb67c5b`

    - Title: Possible problems with remote login using root account
      Summary: OpenSSH configuration file does not explicitly state the option PermitRootLogin in sshd_config file, which will default in RHEL 8 to "prohibit-password".
      Key: `3d21eb9cc1e9cd96e6a4294e771615787299515f`