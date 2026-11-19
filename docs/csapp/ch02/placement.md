---
title: "Ch2 placement quiz"
tags:
  - domain/systems
  - layer/bits
---

# Ch2 placement quiz

One quick question per point, csapp-2-02 to csapp-2-15, to find what I already know. Assume C on x86-64 Linux, 32-bit `int` and two's complement.

**How to use it:** answer every question in one sitting (about 30 min), without reading the book or running code. Then send all answers to Claude, who checks them by running code.

- **Right, and I can say why:** mark the point `can answer` in the [point map](index.md). Skim its sections and do only its code test.
- **Wrong or guessed:** do the full point flow.

| Point | Question |
|---|---|
| 2-02 | `int x = 0x01234567` is stored at address `0x100` on a little-endian machine. Which byte is at `0x100`, `0x101`, `0x102` and `0x103`? |
| 2-03 | `unsigned x = 0xA1B2C3D4`. What are `x ^ ~0xFF` and `x \| 0xFF`? Which one keeps the low byte and flips everything else? |
| 2-04 | `int x = 0x5A, y = 0x0F`. What are `x & y`, `x && y`, `~x \| ~y` and `!x \|\| !y`? Then: `int s = 0xF0000000` (as a bit pattern). What are `s >> 4` and `0xF0000000u >> 4`? |
| 2-05 | What's the unsigned value of the 8-bit pattern `1011 0110`? |
| 2-06 | What's the same pattern's two's-complement value? Why is `-INT_MIN == INT_MIN`? |
| 2-07 | What are `-1 < 0U` and `2147483647U > -2147483647 - 1`? What's wrong with `for (size_t i = n - 1; i >= 0; i--)`? |
| 2-08 | `short sx = -12345;` (`0xCFC7`). What's the hex of `(int)sx`, `(int)(unsigned short)sx` and `(unsigned)sx`? What's `(short)53191`? |
| 2-09 | In 8 bits: what's `100 + 100` signed, and `200 + 100` unsigned? How do you detect unsigned overflow of `s = x + y` using only `s`, `x` and `y`? |
| 2-10 | In 8 bits: what's `-(-128)` signed, `0xFF * 0xFF` unsigned, and `-3 * 50` signed? |
| 2-11 | Write `x * 14` with two shifts and one subtraction. What are `-7 / 4` and `-7 >> 2`? Make the shift version round toward zero. |
| 2-12 | Write 5.875 in binary. What's its 32-bit `float` bit pattern in hex? |
| 2-13 | Which `float` values do the bit patterns `0x00000001`, `0x7F7FFFFF`, `0x7F800000` and `0x7FC00000` encode? |
| 2-14 | Round 2.5, 3.5 and −2.5 to an integer using IEEE round-to-even. What's `(int)(float)16777217`? |
| 2-15 | In `double`, what are `(1e16 + 1) - 1e16` and `(1e16 - 1e16) + 1`? Is `0.1f == 0.1` true? |
