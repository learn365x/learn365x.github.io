---
title: "Notes: 0x and byte order"
tags:
  - domain/systems
  - domain/programming
  - layer/bits
---

# Notes: `0x` and byte order

Reference notes for §2.1.1 and §2.1.3. The worked example is a MODIS LST pixel stored in the two bytes `3A 98`.

## What `0x` means
`0x` marks a number as hexadecimal (base 16). Each hex digit is exactly 4 bits, so two digits make one byte.

| Hex | 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | A | B | C | D | E | F |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| Binary | 0000 | 0001 | 0010 | 0011 | 0100 | 0101 | 0110 | 0111 | 1000 | 1001 | 1010 | 1011 | 1100 | 1101 | 1110 | 1111 |

Hex is only a way to write a value. `0x3A98` always means 15000, on every machine.

```
3    A    9    8
0011 1010 1001 1000
```

## What endianness means
Endianness is the order in which the bytes of a multi-byte value are stored in memory or in a file.

- **Big endian:** the most significant byte comes first, at the lowest address.
- **Little endian:** the least significant byte comes first, at the lowest address.

It reorders **whole bytes**. The bits inside each byte are never reversed.

**Pronunciation:** EN-dee-un (/ˈɛndiən/). The word comes from the egg-cracking war in *Gulliver's Travels* (big end or little end first). Danny Cohen applied it to computers in his 1980 note *On Holy Wars and a Plea for Peace*.

## How to interpret stored bytes
The stored bytes are `3A 98` in both cases. Only the reading differs.

**Read as big endian:** `3A` is the high byte.

```
value = 0x3A98
bit:  15 14 13 12   11 10  9  8    7  6  5  4    3  2  1  0
       0  0  1  1    1  0  1  0    1  0  0  1    1  0  0  0

= 2^13 + 2^12 + 2^11 + 2^9 + 2^7 + 2^4 + 2^3
= 15000
```

**Read as little endian:** `98` is the high byte.

```
value = 0x983A
bit:  15 14 13 12   11 10  9  8    7  6  5  4    3  2  1  0
       1  0  0  1    1  0  0  0    0  0  1  1    1  0  1  0

= 2^15 + 2^12 + 2^11 + 2^5 + 2^4 + 2^3 + 2^1
= 38970
```

Check it by running:

```python
data = bytes([0x3A, 0x98])
for order in ("big", "little"):
    value = int.from_bytes(data, order)
    print(f"{order:6} {value:#06x} {value:016b} {value:5d} {value * 0.02:.1f} K")
```

```
big    0x3a98 0011101010011000 15000 300.0 K
little 0x983a 1001100000111010 38970 779.4 K
```

## Traps
- **Bytes vs value:** say "the bytes `3A 98`" for what is stored. `0x3A98` names a value, so it already assumes an order.
- **Byte swap vs bit reversal:** reversing all 16 bits of `3A 98` gives `0x195C` = 6492, which is neither reading.
- **Bit positions:** count from bit 0 on the right. In a 16-bit value the four groups start at bits 12, 8, 4 and 0.
- **Left is larger, in both orders:** when a value is written in binary, the left bit is always the largest. Endianness doesn't change that.

## Four-byte example: MNIST
An MNIST IDX file starts with the bytes `00 00 08 03`.

| Read as | High byte → low byte | Value |
|---|---|---|
| **Big endian (correct)** | `00 00 08 03` = `0x00000803` | **2051** |
| **Little endian** | `03 08 00 00` = `0x03080000` | **50,855,936** |

Little endian reverses the order of all four bytes. Swapping only the two 16-bit halves gives `08 03 00 00` = `0x08030000` = 134,414,336, which is neither reading.

## Who uses which
- **Little endian (today's mainstream):** x86-64, Apple Silicon, RISC-V, and nearly all ARM systems.
- **Big endian:** IBM Z mainframes, older SPARC and PowerPC, network protocol headers ("network byte order"), and many file formats.

## Example: MODIS LST
MODIS LST products such as MOD11A1 are distributed as HDF4, whose standard numeric types are stored big endian. Libraries such as GDAL convert for you. When reading raw bytes, state the order yourself, and check the header of any exported file:

```python
import numpy as np
lst = np.fromfile("lst.bin", dtype=">u2")  # > = big endian, u2 = uint16
kelvin = lst * 0.02
```

| Bytes `3A 98` read as | Stored value | Temperature (× 0.02) |
|---|---|---|
| **Big endian (correct)** | `0x3A98` = 15000 | **300.0 K** |
| Little endian | `0x983A` = 38970 | 779.4 K |

## Example: TCP port
Network headers are big endian. Port 443 travels as the bytes `01 BB`.

| Bytes `01 BB` read as | Value |
|---|---|
| **Big endian (correct)** | `0x01BB` = **443** |
| Little endian | `0xBB01` = 47873 |

This is why network code converts with `htons()` (host to network) and `ntohs()` (network to host).

## Example: UTF-16
UTF-16 stores most characters in one 16-bit unit, so it has a byte order. A byte order mark at the start of a file can declare it: `FF FE` for little endian, `FE FF` for big endian. UTF-8 works one byte at a time, so it has no byte-order problem.

| Character | UTF-16LE bytes | UTF-16BE bytes | LE bytes wrongly read as BE |
|---|---|---|---|
| `A` (U+0041) | `41 00` | `00 41` | U+4100, a CJK character |
| `中` (U+4E2D) | `2D 4E` | `4E 2D` | U+2D4E, a Tifinagh letter |
