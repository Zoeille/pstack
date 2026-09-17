# Performance Issue Playbook

**Trigger:** Traced slowness. "X is slow", "Y takes too long", latency/throughput regression.

## Steps

1. **Measure baseline.** Before touching anything, get a number. `terminal` with `time`, `hyperfine`, `perf stat`, `curl -w '%{time_total}'`, or app-level timing. Record the exact command and result. No baseline = no fix.

2. **Profile to find the hotspot.** Don't guess. Use the right tool:
   - Python: `cProfile`, `py-spy`, `line_profiler`
   - Node: `--prof`, `clinic`, `0x`
   - General: `perf record`, `strace -c`, `flamegraph`
   - DB: `EXPLAIN ANALYZE`
   
   The profile tells you *where* the time goes. Read it before forming hypotheses.

3. **Form hypotheses, test each.** From the profile, identify 1–3 candidate hotspots. For each:
   - State what you expect to improve and by how much.
   - Make the minimal change to test the hypothesis.
   - Measure. Did it move the number?
   - Keep what works, revert what doesn't.

4. **Implement the fix.** The winning hypothesis becomes the real change. Delegate via `delegate_task` if implementation is mechanical. Keep the change minimal — perf fixes that restructure unrelated code are two PRs.

5. **Measure again.** Same command, same conditions as step 1. Record before/after. The improvement must be real, reproducible, and meaningful.

6. **Commit** with before/after numbers in the commit message.

## Key Rule

No fix without measurement. Before and after numbers are required — in the commit message, not just in your head. "It feels faster" is not evidence.
