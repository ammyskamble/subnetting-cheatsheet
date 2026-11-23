# Subnetting & CIDR Cheat Sheet

Subnetting & CIDR cheat sheet with worked examples — companion to [DevSubnet](https://devsubnet.com), a free client-side subnet calculator.

## Quick Prefix Table

| Prefix | Subnet mask | Total addresses | Usable hosts | Block size |
|--------|-------------|-----------------|--------------|------------|
| /24 | 255.255.255.0 | 256 | 254 | 256 |
| /25 | 255.255.255.128 | 128 | 126 | 128 |
| /26 | 255.255.255.192 | 64 | 62 | 64 |
| /27 | 255.255.255.224 | 32 | 30 | 32 |
| /28 | 255.255.255.240 | 16 | 14 | 16 |
| /29 | 255.255.255.248 | 8 | 6 | 8 |
| /30 | 255.255.255.252 | 4 | 2 | 4 |

## The Two Golden Rules

1. **Usable hosts = 2^(32 - prefix) - 2.** The two addresses you can't use are the network address and the broadcast address. (A /31 is the exception: it has 2 usable addresses and no broadcast, per RFC 3021.)
2. **Allocate the largest subnet first (VLSM).** When splitting a network, always carve out the biggest block first, then the next biggest, and so on — otherwise you'll fragment the address space and run out of room.

## Worked Example: Split 192.168.1.0/24 into Four /26 Subnets

A /26 gives 64 addresses (62 usable hosts), and four /26s exactly fill a /24. The block size is 64, so each subnet starts 64 addresses after the previous one:

| Subnet | Network address | Usable range | Broadcast |
|--------|-----------------|--------------|-----------|
| 1 | 192.168.1.0/26 | 192.168.1.1 - 192.168.1.62 | 192.168.1.63 |
| 2 | 192.168.1.64/26 | 192.168.1.65 - 192.168.1.126 | 192.168.1.127 |
| 3 | 192.168.1.128/26 | 192.168.1.129 - 192.168.1.190 | 192.168.1.191 |
| 4 | 192.168.1.192/26 | 192.168.1.193 - 192.168.1.254 | 192.168.1.255 |

## IPv6 Note

In IPv6 there is no broadcast address and no "minus two" rule. The standard is **/64 per LAN** — every LAN gets a /64, which leaves 64 bits for hosts (2^64 addresses), so you never need to subnet smaller than a /64 for a normal network. Subnetting in IPv6 happens at the /48, /56 and /64 boundaries instead.

## Check Your Math

Want to check your math? Try [DevSubnet — free subnet & CIDR calculator that runs entirely in your browser](https://devsubnet.com). It computes masks, ranges, and usable hosts client-side, so your addresses never leave your browser.
