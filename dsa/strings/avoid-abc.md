Here’s a concise Notion‑ready snippet you can copy straight into your notes:

---

### 📄 Problem Statement

Count the number of strings of length **n**, over the alphabet `{A, B, C}`, that **do not** contain `"ABC"` as a substring.

* **Input:**

  * Integer `n` (length of string)
* **Output:**

  * Number of valid strings

---

### 💡 Key Insight (Recurrence)

Let `f(n)` = valid strings of length `n`.

* **Extend** any valid length-`(n–1)` string by `A/B/C` ⇒ `3·f(n–1)` total.
* **Subtract** those that end in `"ABC"`: you can only append `"ABC"` to any valid length-`(n–3)` string ⇒ `–f(n–3)`.
* **Recurrence:**

  ```text
  f(n) = 3·f(n–1) – f(n–3)
  ```
* **Base cases:** `f(0)=1`, `f(1)=3`, `f(2)=9`.

---

### 🔧 Java Implementation

```java
public class AvoidABC {
    /** 
     * Returns number of length-n strings over {A,B,C} without "ABC".
     */
    public static long countNoABC(int n) {
        if (n == 0) return 1;
        if (n == 1) return 3;
        if (n == 2) return 9;
        long[] dp = new long[n + 1];
        dp[0] = 1; dp[1] = 3; dp[2] = 9;
        for (int i = 3; i <= n; i++) {
            dp[i] = 3 * dp[i - 1] - dp[i - 3];
        }
        return dp[n];
    }

    public static void main(String[] args) {
        // Example usages
        System.out.println(countNoABC(1));  // → 3
        System.out.println(countNoABC(3));  // → 26
        System.out.println(countNoABC(5));  // → 216
    }
}
```

---

### 🧪 Sample Test Cases

| n | Expected Output | Why?                                 |
| - | --------------- | ------------------------------------ |
| 1 | 3               | {"A","B","C"} all valid              |
| 3 | 26              | 3³=27 total, minus “ABC” ⇒ 26        |
| 4 | 75              | 3·f(3)–f(1) = 3·26 – 3 = 78 – 3 = 75 |

---

> **Doc type:**
>
> * **Title:** Avoid “ABC” Substrings
> * **Tags:** `#dp` `#recurrence` `#counting`
> * **Difficulty:** Medium
> * **Approach:** 1D DP with O(n) time & space

