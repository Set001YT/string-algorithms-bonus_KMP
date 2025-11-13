# KMP String Search (Java)

This repository contains a simple, clear Java implementation of the Knuth–Morris–Pratt (KMP) algorithm for substring search.

Files:
- src/KMP.java : KMP implementation and example tests
- sample_input_output.txt : example test inputs and expected outputs
- REPORT.md : short report (implementation, tests, complexity)
- commits.txt : suggested example commits for GitHub

How to compile and run:
1. Ensure you have Java installed (JDK 8+).
2. From repository root:
   - javac src/Main.java
   - java -cp src Main

The program runs three example tests (short, medium, long) and prints occurrence counts, indices, and elapsed time.

Notes:
- The implementation is intentionally minimal and well-commented for clarity.
- Time measurements are coarse and for demonstration only; actual times will vary by machine and JVM.
