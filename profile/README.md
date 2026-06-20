<div align="center">

<img src="https://raw.githubusercontent.com/memahead/.github/main/profile/logo.png" alt="memahead" width="120" />

# memahead

**Agent memory, optimized for what's ahead.**

Compress what your agent remembers based on where it's going — not just where it's been.

<img src="https://raw.githubusercontent.com/memahead/.github/main/profile/architecture.png" alt="memahead architecture" width="700" />

[![PyPI version](https://badge.fury.io/py/memahead.svg)](https://pypi.org/project/memahead/)
[![License](https://img.shields.io/badge/license-Apache%202.0-blue.svg)](https://github.com/memahead/memahead/blob/main/LICENSE)
[![Tests](https://github.com/memahead/memahead/actions/workflows/ci.yml/badge.svg)](https://github.com/memahead/memahead/actions)

---

Most agent frameworks compress context based on what already happened.  
**memahead scores every chunk of memory against the steps still to come** — and drops what future steps won't need.

## Results

Real numbers — reproduce with `python -m benchmarks.run_benchmark`:

| Workflow | Before | After | Saved |
|----------|--------|-------|-------|
| Research & Synthesis | 6,240 tokens | 4,795 tokens | 23% |
| Code Review | 5,386 tokens | 2,113 tokens | 61% |
| Data Analysis | 4,821 tokens | 494 tokens | **90%** |

100% critical fact retention across all workflows.  
Plan-aware compression outperforms Headroom-only by up to **87%**.

Full methodology → [benchmarks/results/README.md](https://github.com/memahead/memahead/blob/main/benchmarks/results/README.md)

Based on [PAACE](https://arxiv.org/abs/2512.16970) and [ACON](https://arxiv.org/abs/2510.00615) — the first production library to implement plan-aware context compression for real agent workflows.

---

### Quick start

```bash
pip install memahead
```

```python
from memahead import Plan, Step, PlanAwareCompressor

plan = Plan([
    Step("research",   "Search and gather raw facts"),
    Step("synthesize", "Identify key themes"),
    Step("draft",      "Write a structured first draft"),
    Step("revise",     "Produce the final polished output"),
])

compressor = PlanAwareCompressor(quality=0.85)

compressed = compressor.compress(
    history=prior_messages,
    tools=all_tool_schemas,
    plan=plan,
    current_step="synthesize",
)

# TokenReport(before=12400, after=3100, saved=9300, compression_ratio=0.75)
print(compressed.report)
```

---

### Repositories

| Repo | Description |
|------|-------------|
| [memahead](https://github.com/memahead/memahead) | Core library |

---

### Links

[memahead.com](https://memahead.com) · [PyPI](https://pypi.org/project/memahead/) · [Discussions](https://github.com/orgs/memahead/discussions)

</div>
