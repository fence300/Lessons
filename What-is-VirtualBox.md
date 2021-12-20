# What is VirtualBox
Virtual Box is a *hypervisor* program.  Basically that means it allows you to run little computers inside of your big computer.  While the little computers are running inside your big computer, your big computer won't have access to the memory or processor cycles that the hypervisor allocates to the little computers.  So, if you have a fancy gaming PC with 32G of RAM, but you start a virtual cluster of 5 Ubuntu instances at 6G each, that leaves only 2G for the host operating system -- so you may notice a significant drop in performance from what you're used to.

# Alternatives
VirtualBox is great for individuals to practice and become familiar with concepts.  If you are going to administrate virtual machines for an enterprise application, you may want to check out:
- ProxMox
- Xen
- VMware
- KVM