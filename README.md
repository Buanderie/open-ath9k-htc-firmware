ath9k_htc research firmware
===========================

This is a modification of the original open-ath9k-htc-firmware for ath9k_htc devices, aimed at providing useful 802.11 debugging / testing tools for 802.11 networking and security researchers. The following list gives an overview of the currently added features:

* Dynamically configure a fixed data rate.
* Set registers on the firmware.
* Read registers from the firmware.
* Print values over USB to dmesg.

These features can be used by any userspace program. Communication between the kernel and the userspace program happens via a Netlink interface instead of the conventional debugfs method. The advantage of this method is that it allows us to conveniently setup a bidirectional communication channel between the firmware and the application. Only one interface to a device is currently supported. Please feel free to submit a pull request if you think you have a feature that could be helpful for other researchers.


Installation
------------

1. Compile the firmware.
2. Go to your firmware directory, usually `/usr/lib/firmware/`.
3. Backup `htc_9271.fw`.
4. Copy the research firmware.
5. Compile my modified driver kernel modules ([github.com/rpp0/linux](https://github.com/rpp0/linux)). To do this, build the entire kernel from my repo, set as alternative kernel in GRUB, and boot it from your machine or VM, then run the `makeath9k` script. This script will build and swap the driver modules. Alternatively, you could also `grep` the git log for your Linux version, rebase the research branch to that commit, and then run `makeath9k`.

Note: Permanently installing the modified modules is not recommended, unless you are working in a VM which don't mind crashing; please run the module swap script `makeath9k` instead.


Disclaimer
----------

Though I have tested all committed code, I cannot guarantee that all aspects of the firmware or driver will keep working as intended, and I have only have one system to test. Kernel crashes could therefore happen, so use at your own risk!