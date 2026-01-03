# OEIS-A079777-c

This repository contains C implementations related to OEIS sequence
[A079777](https://oeis.org/A079777).

The sequence is defined by the recurrence

    a(0) = a0
    a(1) = a1
    a(n) = (a(n-1) + a(n-2)) mod n   for n >= 2

(Initial values are provided at runtime.)

---

## Contents

- `slow_reference.c`  
  A simple, obviously-correct reference implementation that computes
  the sequence directly from the definition. This version is fairly slow
  and is intended only for verification.

- `fast.c`  
  An optimized implementation that combines two modular steps at once
  and avoids the `%` operator in the inner loop. This version was used
  to search for zero terms up to n = 25×10^13.

---

## Verification strategy

The optimized implementation was validated as follows:

- Cross-checked against `slow_reference.c` for small and medium ranges.
- Algebraic equivalence with the defining recurrence was verified.
- Boundary cases (interval endpoints, parity of ranges) were examined
  carefully due to the two-step update logic.

Despite extensive testing, independent verification is strongly encouraged.

---

## Results

Using `fast.c`, all indices n ≤ 25×10^13 for which a(n) = 0 were searched.
The results agree with previously known terms a(1)-a(35) in the OEIS entry and produce two new terms. Namely a(36) = 80388574032397 and a(37) = 159771475111875.

If additional zero terms are known beyond this range,
or if discrepancies are found, please open an issue or contact me.

---

## Build & usage

Compile with a modern C compiler (gcc or clang):

    gcc -O3 fast.c -o fast
    gcc -O2 slow_reference.c -o slow

Run and follow the prompts to specify the range and initial conditions.

---

## Notes

This code is written with the goal of producing reliable, repeatable results rather than extreme performance.
The faster version makes some assumptions that are explained in the comments, so please read those carefully before modifying the code.

---

## License

Public domain / CC0.
