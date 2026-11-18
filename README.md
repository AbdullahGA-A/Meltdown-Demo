For our report, we ran the exploit demo code on a VMware Workstation Virtual Machine running Ubuntu 16.04 with two cores and 6 Gigabytes of RAM. (Cores can be reduced to 1).
Before the exploitation is run, KPTI and KASLR must be disabled.

To disable KASLR and KPTI, add the flags "nokaslr", "nopti" and "pti=off"(for good measure) to the Linux command line. This can be done through the command "sudo nano /etc/default/grub" by adding all three flags to the end of the field "GRUB_CMDLINE_LINUX" or "GRUB_CMDLINE_LINUX_DEFAULT".

Run the command "sudo update-grub" and reboot the machine (either through the "reboot" command or your own personal preference). If the message "KASLR disabled" appears, then you have successfully run the Linux boot command.

To check if your computer is vulnerable to Meltdown, run the command "cat /sys/devices/system/cpu/vulnerabilities/meltdown".

Now find where the meltdown-demos files are in the Ubuntu Instance and run "make" to compile them all!

Test: 
"taskset 0x1 ./test" to test Meltdown within the same address space.

Physical_reader:
run the command "sudo ./secret" in one terminal and "taskset 0x1 ./physical_reader [address of secret]" in another.[address of secret] is the address presented by the first terminal.

memdump:
Run the command "sudo ./secret" in one terminal and "taskset 0x1 ./memdump [address of secret] 50" in another. This command will read the first 50 bytes from the address.

reliability:
Run the command "taskset 0x1 ./reliability" to check the reliability of Meltdown on your own computer.  


For more methods, consult the FAQ on the original Meltdown repository here: (https://github.com/isec-tugraz/meltdown/tree/master)
or explore the libkdump.c file and change the definition of MELTDOWN (line 113) to meltdown, meltdown_nonull, or meltdown_fast.
