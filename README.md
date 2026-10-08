# ASOLARIA CIVILISATION — THE SHARED MATRIX

Fifteen agents, one surface, **729 cells** (27² — the ternary lattice squared). Every agent grows
this matrix and can bump into another agent's work.

## Time is a hash chain, not a clock

```
tick[0] = sha16("TICK|" + agent_pid + "|0")
tick[k] = sha16(tick[k-1] + "|" + agent_pid + "|" + k)
```

Each agent is given **600 ticks = 10 minutes**. The sequence is deterministic and reproducible
**from the agent's PID alone**, so the whole civilisation runs instantly and the schedule stays
auditable. Time was skipped; **the work was not** — every tick read real bytes and verified them
against `.sha256` sidecars written by other people. **4,917,706,148 bytes read.**

## The rules

- **CREATE-ONLY.** The first writer keeps the cell. There is no delete verb and no overwrite verb
  in the kernel. The matrix can only get bigger — the one property that makes a shared surface safe
  for strangers.
- **A collision is a BUMP**, recorded with both agents, both ticks and both payload digests.
  **`overwritten=0`, `dropped=0`** across 7,946 bumps.
- **The act is derived from the tick's own hash** — research / chariot / fix / improve / read /
  write — so no agent can prefer the easy work.

## Result

```
agents=15  ticks_each=600  ticks_total=9,000
cells_grown=729/729  saturated
bumps=7,946  overwritten=0  dropped=0
gimel=7,729  shin=1,150  bytes_read=4,917,706,148
```

## The flaw this run exposed — stated, not hidden

**Cells were decided by roster order, not by merit.** Because each agent's full ten minutes ran to
completion before the next agent started, the first agent took 409 of 729 cells and **six agents
got zero** — their scoreboard rows read `could_not_do=grow a single uncontested cell`. They bumped
600 times each and grew nothing.

The hash-time skip serialised what concurrency would have interleaved. The honest fix is a **global
tick order** across all agents rather than per-agent sequential schedules. Recorded here beside the
result rather than quietly re-run.

Measured by **ACER-CLAUDE-FABLE5** · pid `8467a937cba309f7` · owner **OP-JESSE** · `E=0` · `json=0`
