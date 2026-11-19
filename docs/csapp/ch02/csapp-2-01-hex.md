---
title: "Hex is shorthand for bits; data sizes come from the ABI, not from C"
id: csapp-2-01
type: concept
source: "CSAPP 3e §2.1.1–2.1.2"
year:
learned:
status:
needs: []
unlocks: [csapp-2-02, csapp-2-03, csapp-2-05]
tags:
  - domain/systems
  - domain/programming
  - layer/bits
---

# Hex is shorthand for bits; data sizes come from the ABI, not from C

## 1. Questions
Answer first, without reading. No calculator for 1–5. Write your answers here, then send them to Claude to check.

1. Write `0x39A7F8` in binary.

2. Write `1100 1001 0111 1011` in hex.

3. Write 2²³ in hex. What is `0x2000` in decimal?

4. Work these out in hex: 167 (decimal → hex), `0x503C + 0x8`, `0x503C − 0x40`.

5. A machine has 64-bit virtual addresses. How many bytes can it address? What is the highest address in hex? How many hex digits does a 64-bit value take?

6. Fill in `sizeof` (in bytes) for **Linux x86-64** and **Windows x64**: `char`, `short`, `int`, `long`, `long long`, `void *`, `float`, `double`, `size_t`.

7. What does `printf("%ld\n", (long)3000000000LL);` print on each platform?

8. Your PyTorch model has 1 billion parameters. How many bytes does it take in fp32, fp16/bf16 and int8? Is 2 GB more or less than 2 GiB? Why do some CUDA kernels break when a tensor has more than `0x7FFFFFFF` elements?

## 2. If stuck, read
- CSAPP §2.1.1 (hex notation, including the 2ⁿ trick) and §2.1.2 (data sizes, Figure 2.3). Then re-answer the questions above.

## 3. Predict, then run
Run this on Linux (WSL or the server): `gcc -Wall -o sizes sizes.c && ./sizes`. Write down your prediction for each line first. If you also have a Windows compiler, run it there too and compare.

```c
#include <stdio.h>
#include <stdint.h>
int main(void) {
    printf("char %u short %u int %u long %u llong %u ptr %u size_t %u\n",
           (unsigned)sizeof(char), (unsigned)sizeof(short), (unsigned)sizeof(int),
           (unsigned)sizeof(long), (unsigned)sizeof(long long),
           (unsigned)sizeof(void *), (unsigned)sizeof(size_t));
    printf("%ld\n", (long)3000000000LL);
    printf("%#x %#x %#x\n", 0x503C + 0x8, 0x503C - 0x40, 1 << 23);
    return 0;
}
```

**My prediction:** ...

**Actual output:** ...
**Prediction right?** yes / no, and why

## 4. Summary (my own words)
- ...

## 5. Big picture
**Shared principle:** a number's width is fixed by a contract outside the language (the ABI, a file format, a dtype), and code that assumes a different width breaks silently.

| Field | Same principle there | Check question | Verified? |
|---|---|---|---|
| ML dtypes | Model memory = parameter count × dtype width | What's the size of a 7B model in bf16, in GiB? | |
| CUDA / PyTorch | `int32` vs `int64` index width limits tensor size | Why does `torch.int32` overflow at `numel() > 2**31 - 1`? | |
| Networking | IPv4 addresses are 32 bits, IPv6 addresses are 128 bits written in hex groups | How many hex digits are in a full IPv6 address? | |

## 6. Mistakes log
- yyyy-mm-dd: I thought ___, actually ___.
