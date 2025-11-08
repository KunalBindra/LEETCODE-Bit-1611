# LEETCODE-Bit-1611
---

# ✅ **Understanding the Purpose**
So let’s dry-run it step by step.

---

# ✅ **Pre-computation: The func array**

```java
long[] func = new long[32];
func[0] = 1;
for (int i = 1; i <= 31; i++) {
    func[i] = 2 * func[i - 1] + 1;
}
```

This builds the sequence:

```
func[0] = 1
func[1] = 3
func[2] = 7
func[3] = 15
func[4] = 31
...
func[i] = 2^(i+1) - 1
```

So func[i] = (1 << (i+1)) - 1.

---

# ✅ **Core Logic Dry Run (Generic Explanation)**

```java
int result = 0;
int sign = 1;
for (int i = 30; i >= 0; i--) {
    int ith = ((1 << i) & n);
    if (ith == 0) continue;
    if (sign > 0) result += func[i];
    else result -= func[i];
    sign *= -1;
}
return result;
```

The loop scans bits from **MSB → LSB**.
For each set bit `i`:

1. Add or subtract `func[i]` based on alternating sign
2. Flip the sign

This is basically converting the binary representation into the Gray-code move count.

---

# ✅ **Now… Dry Run With an Example**

Tell me **which value of n** you want to dry-run (common test values: 1, 3, 6, 9, 11, 13, 17…).

For instance:

If you say: **dry run for n = 6**,
I’ll give you a clear step-by-step:

Bits of 6 → `110`
i = 2 → result = +7
i = 1 → result = 7 - 3 = 4
i = 0 → skip
Final result = 4 ✅

---
