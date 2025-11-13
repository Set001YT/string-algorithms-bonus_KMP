# KMP Implementation Report

Summary
-------
I implemented the Knuth–Morris–Pratt (KMP) substring search algorithm in Java. The implementation includes:
- buildLPS: builds the LPS (longest proper prefix which is also suffix) array for the pattern.
- search: uses the LPS array to search for all occurrences of a pattern in a text in linear time.
- A main method that runs three example tests: a short string, a medium-length string, and a long string constructed by repeating a short unit.

Implementation notes
--------------------
- The KMP algorithm avoids re-examining characters in the text by using the LPS array to know how much to shift the pattern when a mismatch occurs.
- The code is intentionally simple and documented with minimal, clear comments.
- The search method returns 0-based starting indices for each match; an empty pattern is treated as matching at every position (conventional behavior).

Tests
-----
Three test cases illustrate behavior under different input sizes:

1. Short
   - Text: "abababab" (length 8)
   - Pattern: "ab" (length 2)
   - Expected occurrences: 4 at indices [0, 2, 4, 6]
   - Result: occurrences found as expected.

2. Medium
   - Text: "abxabcabcaby" (length 12)
   - Pattern: "abcaby" (length 6)
   - Expected occurrences: 1 at index [6]
   - Result: occurrences found as expected.

3. Long
   - Text: "abcde" repeated 2000 times (length 10,000)
   - Pattern: "cdeab"
   - Expected occurrences: 2000 (one per repetition, starting at index 2 within each repeated unit)
   - Result: occurrences found as expected. Runtime scales linearly with text length.

Complexity analysis
-------------------
Let n = length of text, m = length of pattern.

- Building LPS array: O(m) time, O(m) space.
  - We compute lps[0..m-1] by scanning the pattern once and using previously computed lps values for fallbacks.

- Searching: O(n) time in the worst-case, O(1) extra space (not counting the output list).
  - The search loop advances through the text only once; whenever a mismatch occurs, the algorithm uses the lps array to shift the pattern without moving the text index back.
  - Combined with LPS building, total time is O(n + m).

- Space:
  - O(m) for the LPS array.
  - O(k) for output storage (k = number of matches); otherwise constant additional workspace.

Practical notes
---------------
- KMP is deterministic and guarantees linear worst-case runtime, unlike some hashing-based methods (e.g., Rabin-Karp) which may have rare collisions and require rechecks.
- For many practical uses (e.g., searching for single patterns), modern Java libraries like String.indexOf are optimized, but KMP is a good didactic and robust algorithm when implementing string search from scratch or when you need deterministic linear behavior.

How to reproduce
----------------
- Compile and run the included `src/Main.java` as described in README.md.
- The program prints counts, example match indices, and rough timings (measured using System.nanoTime).

Conclusions
-----------
The KMP algorithm provides robust linear-time pattern searching. The implementation here is compact, easy to read, and suitable for educational use or integration into small projects where a custom, deterministic substring search is needed.
