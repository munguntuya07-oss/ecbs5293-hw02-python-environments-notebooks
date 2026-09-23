# Diagnosis notes

**One five-part note per failure you fixed.** This file is laid out with a section for each of
the two failure families. That is the default shape, not a rule — any organisation that gives
every cause its own evidence is fine.

Part 3 must be **raw output you actually ran**, pasted, not a description of it.

**Open this file before you start fixing anything.** Once a repair works, the error that proved
the cause is gone and you cannot get it back without breaking the project again. Paste each
traceback into part 3 the moment you see it; write the rest afterwards.

---

## Note 1 — Environment

1. **What was the symptom?**
the project was giving an error when i tried to run the code. At first i though the problem was the Python was using the wrong environment or kernel
2. **What was the actual cause?**
the issue was related to Python environment being used by project. I needed to check which Python executable was actually being used in the terminal and in the notebook, and alsi check the pyproject.toml

3. **What evidence showed that?**

   This note needs both of these, and you have to say which window each came from:

   - `sys.executable` from `uv run python -c "..."` in the terminal
     File "/Users/moana/fall_2026/data_science/ecbs5293-hw02-python-environments-notebooks/scripts/report.py", line 8, in <module>
    import pandas as pd
ModuleNotFoundError: No module named 'pandas'
   - `sys.executable` from a notebook cell
        File "/Users/moana/fall_2026/data_science/ecbs5293-hw02-python-environments-notebooks/scripts/report.py", line 8, in <module>
    import pandas as pd
ModuleNotFoundError: No module named 'pandas'

   Then say whether the two paths match, and what that does and does not tell you. Matching
   paths rule out a wrong kernel. They say nothing about what the project *declares* — that
   is a separate question, answered by reading `pyproject.toml`.

   Paste the raw output, plus the traceback lines that started you off:

   ```the two paths match, this rules out a wrong notebook kernel, however matching paths do not tell me what the project declares, i checked pyproject.toml separately where pandas>=2.3.3 is already listed.


   ```

4. **What did you change?**
i checked environment and added the required pandas dependecy to environment. 

5. **How did you verify it worked?**
I ran the project after fixing it, the ModuleNotFoundError was gone.
---

## Note 2 — Notebook state

1. **What was the symptom?**
notebook wasn't giving the expected results when i ran the cells. The results depended on variables in previious cells, so it could affect the output

2. **What was the actual cause?**
the problem was caused by order of cells and the order in which cells the had been run.

3. **What evidence showed that?**

   Paste the raw output, saying which window each line came from — the tracebacks from the
   clean run, and anything you ran to find out what a cell depended on:

   ``
NameError                                 Traceback (most recent call last)
Cell In[2], line 1
----> 1 by_product = df.groupby("product")["revenue"].sum()
      2 significant = by_product[by_product > threshold]
      3 significant.round(2)

NameError: name 'df' is not defined
   ```
   This shows variable df depended on previous one.

4. **What did you change?**
I added import sys ; print(sys.executable) and reoderded the cells, made sure every cells are working by running them one by one. 

5. **How did you verify it worked?**
-i ran the notebook again from the beginning and compared it with the script
-before the threshold filter, the revenue for each product was the same to the cent in both the script and the notebook
-then i checked the products selected by the notebook. they were exactly the products with revenue above 1000 in the table
-i also checked the formula used to calculate the revenue

   This part carries the **reconciliation**. State both:

   - the script's per-product revenue table and the notebook's per-product revenue, *before*
     the threshold filter, agree to the cent;
   - the products the notebook selects are exactly those above 1,000 in that table.

   Agreement shows the two implementations agree on the numbers. It does not by itself prove
   the shared formula is right — so say what you checked, and no more.
