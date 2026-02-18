Investigate this issue using the competing hypotheses method: $ARGUMENTS

**Process:**

1. Analyse the issue description and generate 3-5 distinct hypotheses about the root cause. Each hypothesis should be plausible but different in nature (e.g., one about data, one about timing, one about configuration, one about logic errors).

2. Create an agent team and spawn one `investigator` teammate per hypothesis. Each teammate should:
   - State their hypothesis clearly
   - Search the codebase for evidence supporting or refuting it
   - Try to find evidence that DISPROVES their hypothesis (not just confirms it)
   - Report: evidence for, evidence against, confidence level (high/medium/low), and what would definitively prove/disprove it

3. After all investigators report, have them message each other to debate:
   - Can any hypothesis be ruled out?
   - Do multiple hypotheses point to the same root cause?
   - Is there a hypothesis no one considered?

4. Synthesise into a final report:
   - Most likely root cause (with confidence)
   - Evidence summary
   - Suggested fix
   - How to verify the fix resolves the issue
   - What to monitor after fixing
