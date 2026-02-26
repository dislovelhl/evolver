# 🧬 Capability Evolver

![Capability Evolver Cover](assets/cover.png)

**[evomap.ai](https://evomap.ai)** | [Documentation](https://evomap.ai/wiki) | [Chinese Docs](README.zh-CN.md)

---

## At a Glance

**"Evolution is not optional. Adapt or die."**

- **What it is**: A protocol-constrained self-evolution engine for AI agents
- **Problem it solves**: Turns ad hoc prompt tweaks into auditable, reusable evolution assets with a clear audit trail
- **Get started in 30 seconds**: `npm install` → `node index.js` to generate a GEP-guided evolution prompt

---

## Quick Start

### Prerequisites

- **Node.js**: v14.0.0 or higher
- **npm**: v6.0.0 or higher
- **Git**: for repository operations and log inspection

### Installation

```bash
# Clone the repository
git clone https://github.com/dislovelhl/evolver.git
cd evolver

# Install dependencies
npm install

# Build the project
npm run build
```

### Your First Evolution (5 minutes)

```bash
# Run your first evolution
node index.js
```

**What happens:**
1. The evolver scans your runtime logs and history files
2. It extracts signals (errors, patterns, performance issues)
3. It selects or recommends a Gene (reusable fix)
4. It emits a **GEP-guided prompt** that tells you exactly how to improve your agent
5. You review the prompt and apply the changes with confidence

---

## What It Does

The **Capability Evolver** inspects runtime history, extracts signals, selects a Gene/Capsule, and emits a strict GEP protocol prompt to guide safe evolution.

---

## Who This Is For / Not For

### ✅ This Is For You If:

- You maintain AI agent prompts and logs at scale
- You need auditable evolution traces (Genes, Capsules, EvolutionEvents)
- Your environment requires deterministic, protocol-bound changes
- You want to turn one-off fixes into reusable, documented assets

### ❌ Not Ideal For:

- One-off scripts without logs or history
- Projects requiring free-form creative changes without audit trails
- Systems that cannot tolerate protocol overhead
- Environments without git or file system access

---

## Core Concepts

### 🧬 Gene

A **reusable, validated code transformation or fix** stored in `assets/gep/genes.json`.

**Structure:**
```json
{
  "id": "fix-async-timeout",
  "name": "Fix Async Timeout Error",
  "description": "Adds timeout wrapper to prevent hanging async calls",
  "category": "stability",
  "validation": [
    "npm test --grep='async'",
    "node scripts/validate-timeout.js"
  ],
  "payload": "// Code transformation here"
}
```

### 💊 Capsule

A **higher-level bundle of related Genes** for solving a specific problem domain, stored in `assets/gep/capsules.json`.

### 📊 EvolutionEvent

An **audit log entry** recording each evolution run, stored in `assets/gep/events.jsonl`.

### 🔬 GEP Protocol (Genome Evolution Protocol)

A **standardized format for safe, auditable evolution** ensuring only validated transformations are applied.

---

## Features

### Core Capabilities
- **Auto-Log Analysis**: Scans memory and history files for errors and patterns
- **Smart Signal Extraction**: Identifies recurring problems automatically
- **GEP Protocol**: Standardized evolution with reusable, auditable assets
- **Self-Repair Guidance**: Emits repair-focused directives from signals
- **Protected Source Files**: Prevents autonomous agents from overwriting core evolver code

### Developer Features
- **Mutation + Personality Evolution**: Each evolution run is gated by an explicit Mutation object and evolvable PersonalityState
- **Configurable Strategy Presets**: `EVOLVE_STRATEGY=balanced|innovate|harden|repair-only` controls intent balance
- **Signal De-duplication**: Prevents repair loops by detecting stagnation patterns
- **Operations Module** (`src/ops/`): Portable lifecycle, skill monitoring, cleanup, self-repair, wake triggers—zero platform dependency
- **One-Command Evolution**: `node index.js` to generate the prompt

---

## Usage

### Standard Run (Automated)

```bash
node index.js
```

### Review Mode (Human-in-the-Loop)

```bash
node index.js --review
```

### Continuous Loop

```bash
node index.js --loop
```

### With Strategy Presets

```bash
# Maximize new features
EVOLVE_STRATEGY=innovate node index.js --loop

# Focus on stability
EVOLVE_STRATEGY=harden node index.js --loop

# Emergency fix mode
EVOLVE_STRATEGY=repair-only node index.js --loop
```

### Operations & Lifecycle Management

```bash
node src/ops/lifecycle.js start    # start evolver loop in background
node src/ops/lifecycle.js stop     # graceful stop
node src/ops/lifecycle.js status   # show running state
node src/ops/lifecycle.js check    # health check + auto-restart if stagnant
```

---

## Typical Use Cases

- Harden a flaky agent loop by enforcing validation before edits
- Encode recurring fixes as reusable Genes and Capsules
- Produce auditable evolution events for review or compliance

---

## Anti-Examples (What NOT to Do)

- Rewriting entire subsystems without signals or constraints
- Using the protocol as a generic task runner
- Producing changes without recording EvolutionEvent

---

## Project Structure

```
evolver/
├── assets/
│   └── gep/
│       ├── genes.json          # Reusable transformations
│       ├── capsules.json       # Bundled Genes
│       └── events.jsonl        # Audit trail
├── src/
│   ├── evolve.js              # Core evolution engine
│   ├── gep/
│   │   ├── prompt.js          # GEP protocol prompt assembly
│   │   ├── selector.js        # Gene/Capsule selection logic
│   │   └── solidify.js        # Validation command execution
│   └── ops/
│       └── lifecycle.js        # Lifecycle management
├── scripts/
│   ├── a2a_ingest.js          # External asset ingestion
│   └── a2a_promote.js         # Asset promotion
├── index.js                    # Main entry point
└── README.md
```

---

## Configuration & Customization

### Environment Variables

```bash
EVOLVE_REPORT_TOOL=feishu-card
EVOLVE_STRATEGY=harden
DEBUG=evolver:*
```

### Local Overrides (Injection)
You can inject local preferences without modifying core code.

**Method 1: Environment Variables**
```bash
EVOLVE_REPORT_TOOL=feishu-card
```

**Method 2: Dynamic Detection**
The script automatically detects if compatible local skills exist in your workspace.

---

## FAQ

**Does this edit code automatically?**
No. It generates a protocol-bound prompt and assets that guide evolution.

**Do I need to use all GEP assets?**
No. You can start with default Genes and extend over time.

**Is this safe in production?**
Use review mode and validation steps. Treat it as a safety-focused evolution tool, not a live patcher.

---

## Troubleshooting

### Installation Issues

**Problem:** npm install fails with permission errors

**Solution:**
```bash
npm cache clean --force
npm install -g npm@latest
npm install
```

**Problem:** Node version incompatibility

**Solution:**
```bash
node --version  # Ensure v14.0.0 or higher
nvm install 18
nvm use 18
```

### Runtime Issues

**Problem:** Cannot find logs or history files

**Solution:**
- Ensure your agent writes logs to the expected location
- Check the log file paths in your configuration
- Run with `DEBUG=evolver:*` to see paths

**Problem:** Evolution loop hangs or times out

**Solution:**
```bash
node src/ops/lifecycle.js check
node src/ops/lifecycle.js stop
node src/ops/lifecycle.js start
```

---

## Security Model

### What Executes and What Does Not

| Component | Behavior | Executes Shell Commands? |
| :--- | :--- | :--- |
| `src/evolve.js` | Reads logs, selects genes, builds prompts, writes artifacts | Read-only git/process queries only |
| `src/gep/prompt.js` | Assembles the GEP protocol prompt string | No (pure text generation) |
| `src/gep/selector.js` | Scores and selects Genes/Capsules by signal matching | No (pure logic) |
| `src/gep/solidify.js` | Validates patches via Gene validation commands | Yes (see below) |
| `index.js` (loop recovery) | Prints sessions_spawn(...) text to stdout on crash | No (text output only) |

### Gene Validation Command Safety

All validation commands are gated by a safety check:

1. **Prefix whitelist**: Only commands starting with `node`, `npm`, or `npx` are allowed
2. **No command substitution**: Backticks and `$(...)` are rejected
3. **No shell operators**: `;`, `&`, `|`, `>`, `<` are rejected
4. **Timeout**: Each command is limited to 180 seconds
5. **Scoped execution**: Commands run with `cwd` set to the repository root

### A2A External Asset Ingestion

External Gene/Capsule assets are staged in an isolated zone. Promotion requires:

1. Explicit `--validated` flag
2. All validation commands are audited against safety checks
3. Gene promotion never overwrites existing Genes with the same ID

---

## Public Release & Versioning

### Building & Publishing

```bash
npm run build
npm run publish:public
DRY_RUN=true npm run publish:public  # Dry run
```

### Required Environment Variables

- `PUBLIC_REMOTE` (default: `public`)
- `PUBLIC_REPO` (e.g., `dislovelhl/evolver`)

### Semantic Versioning

MAJOR.MINOR.PATCH
- MAJOR: incompatible changes
- MINOR: backward-compatible features
- PATCH: backward-compatible bug fixes

---

## Changelog

See the full release history on [GitHub Releases](https://github.com/dislovelhl/evolver/releases).

---

## Roadmap

- Add a one-minute demo workflow
- Add a comparison table vs alternatives
- Add webhook integration for external evolution triggers
- Add mutation testing framework

---

## Acknowledgments

- [onthebigtree](https://github.com/onthebigtree) -- Inspired the creation of evomap evolution network
- [lichunr](https://github.com/lichunr) -- Contributed thousands of dollars in tokens for our compute network to use for free
- [shinjiyu](https://github.com/shinjiyu) -- Submitted numerous bug reports for evolver and evomap
- [upbit](https://github.com/upbit) -- Played a vital role in popularizing evolver and evomap technologies
- [Chi Jianqiang](https://mowen.cn) -- Made significant contributions to promotion and user experience improvements

More contributors to be added.

---

## License

MIT

---

## Further Reading

- 📖 [Full Documentation](https://evomap.ai/wiki)
- 🌐 [EvoMap Platform](https://evomap.ai)
- 🇨🇳 [中文文档](README.zh-CN.md)