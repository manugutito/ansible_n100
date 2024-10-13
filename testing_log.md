# After updating and upgrading and installing minidlna, openSeaChest, powertop and samba

- Power: ~26 W with both HDDs in Idle_B, ~22 W with both HDDs in standby_z.
- Package C states: C2 (pc2) 0.6%, C3 (pc3) 97.7%

# After running powertop --auto-tune

- Power: ~21 W with both HDDs in standby_z
- Package C states: very similar (95+% C3)

# ASPM for Realtek

Run the [one-liner](https://www.youtube.com/watch?v=-DSTOUOhlc0&t=536s)

```
sudo lspci -vv | awk '/ASPM/{print $0}' RS= | grep --color -P '(^[a-z0-9:.]+|ASPM)
```

to have a look at the ASPM states of different PCI buses.

We can force ASPM on the Realtek NIC by changing this to a one:

```
$ cat /sys/bus/pci/drivers/r8169/0000\:02\:00.0/link/l1_aspm
0
```

After this:

- Power: ~19 W with the HDDs in standby_z
- Package C states: 95+% in C10!