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

# Installing ZFS

After installing ZFS and running `zpool import` to detect the status of the pool, the disks spin up and go back to Idle_b. The Power is then 25 W (in like with the results before reinstalling).

Spinning the disks down by hand with openSeaChest brings the power consumption back down to ~19 W.

# Identifying the problem

Using iotop we can identify which process is doing I/O:

```
Total DISK READ:       484.47 M/s | Total DISK WRITE:        11.47 K/s
Current DISK READ:     485.43 M/s | Current DISK WRITE:      19.12 K/s
    TID  PRIO  USER    DISK READ>  DISK WRITE    COMMAND
  17171 be/0 root      162.17 M/s    0.00 B/s [z_rd_int]
  17172 be/0 root      118.19 M/s    0.00 B/s [z_rd_int]
  17148 be/0 root      114.61 M/s    0.00 B/s [z_rd_int]
  17317 be/7 root       89.51 M/s    0.00 B/s [dsl_scan_iss]
```

And googling `z_rd_int` solves the problem:

```
$ sudo zpool status myzpool
  pool: myzpool
 state: ONLINE
  scan: scrub in progress since Sat Oct 12 22:24:01 2024
```

So it should literally go away on its own. Funny how the scrub persisted through two Ubuntu reinstalls!
