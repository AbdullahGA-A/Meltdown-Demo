For our report, we ran the exploit demo code on a VMware Workstation Virtual Machine running Ubuntu 16.04 with two cores and 6 Gigabytes of ram. (cores can be reduced to 1).
before the exploitation is ran, KPTI and KASLR must be disabled.

in order to disable KASLR and KPTI the flags "nokaslr" "nopti" and "pti=off"(for good measure) to the Linux command line, this can be done through the command "sudo nano /etc/default/grub" and adding all three flags to the end of the field "GRUB_CMDLINE_LINUX" or "GRUB_CMDLINE_LINUX_DEFAULT".

run the command "sudo update-grub" and reboot the machine (either through the "reboot" command or your own personal preference). if the message:"KASLR disabled" appears, then you have successfully ran the linux boot command.

to check if your computer is vulnerable to meltdown, run the command "cat /sys/devices/system/cpu/vulnerabilities/meltdown".

now find where the meltdown-demos files are in the Ubuntu Instance and run "make" to compile all them!

Test: 
"taskset 0x1 ./test" to test meltdown within the same address space.

Physical_reader:
run the command "sudo ./secret" in one terminal and "taskset 0x1 ./physical_reader [address of secret]" in another.[address of secret] is the address presented by the first terminal.

memdump:
run the command "sudo ./secret" in one terminal and "taskset 0x1 ./memdump [address of secret] 50" in another. this command will read the first 50 bytes from the address.

reliability:
run the command "taskset 0x1 ./reliability" to check the reliability of meltdown in your own computer.  


for more methods, consult the FAQ on the original meltdown Repository here: (https://github.com/isec-tugraz/meltdown/tree/master)
or explore the libkdump.c file and change the definition of MELTDOWN (line 113) to meltdown, meltdown_nonull, or meltdown_fast.