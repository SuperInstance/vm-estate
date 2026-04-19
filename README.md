# VM-Estate

> **"Each machine is a plot of land. Intelligence grows on that land. Add more plots = more intelligence."**
> — Casey Digennaro

VM-Estate is a play on real estate. Instead of land, we're developing **compute plots** — machines that grow intelligence through continuous learning. The more plots you add, the smarter the fleet becomes. Not linearly — exponentially.

## The Core Idea

Traditional AI: One big model, one big machine, one big training run.

VM-Estate: Many small models, many small machines, continuous distributed training. Each node specializes. Nodes share **thinking patterns** (LoRA adapters), not just data. The fleet becomes a distributed cognitive system.

## Architecture

```
                    ┌─────────────────┐
                    │   Oracle1 🔮     │
                    │  Coordination    │
                    │  Tile Server     │
                    │  Quality Gate    │
                    │  Port 8847       │
                    └────────┬────────┘
                             │
              ┌──────────────┼──────────────┐
              │              │              │
    ┌─────────▼──────┐ ┌────▼────────┐ ┌──▼──────────────┐
    │ Forgemaster ⚒️  │ │ JC1 🔧      │ │ JC2-N (future)   │
    │ RTX 4050        │ │ Jetson Orin │ │ Jetson / Cloud   │
    │                 │ │             │ │                  │
    │ Specialization: │ │ Specializ.: │ │ Specialization:   │
    │ - Kernel traces │ │ - CUDA exps │ │ - Assigned by     │
    │ - Forge pipeline│ │ - Edge inf. │ │   fleet topology  │
    │ - Crate arch    │ │ - HW constr.│ │                  │
    │                 │ │             │ │                  │
    │ Emits:          │ │ Emits:      │ │ Emits:           │
    │ kernel-adapter  │ │ edge-adapter│ │ domain-adapter    │
    └────────┬────────┘ └────┬────────┘ └────────┬─────────┘
             │               │                    │
             └───────────────┼────────────────────┘
                             │
                    ┌────────▼────────┐
                    │  Adapter Market │
                    │  (Oracle1)      │
                    │  Validate ≥0.94 │
                    │  Tag & Distribute│
                    └─────────────────┘
                             │
                    All nodes pull validated adapters
                    → Load into inference runtime
                    → Gain expertise they never trained on
                    → That's distributed cognition
```

## How Intelligence Scales

### The Math

| Nodes | Training Capacity | Overnight Steps | Adapter Diversity | Fleet IQ |
|-------|-------------------|-----------------|-------------------|----------|
| 1 | 1.7 steps/s | ~50K | 1 adapter | Baseline |
| 3 (current fleet) | ~5 steps/s | ~150K | 3 adapters | 3x coverage |
| 10 | ~17 steps/s | ~500K | 10 adapters | 10x domains |
| 50 | ~85 steps/s | ~2.5M | 50 adapters | Full coverage |
| 100 | ~170 steps/s | ~5M | 100 adapters | Redundant intelligence |

### Why Exponential, Not Linear

Each new node doesn't just add training capacity. It adds:

1. **New specialization** — training on data no other node has
2. **New adapter** — a thinking pattern no other node developed
3. **Cross-pollination** — every other node can load this new adapter
4. **Redundancy** — if any node dies, its adapter survives on other nodes

So adding node N gives N-1 other nodes a new capability. That's O(N²) capability growth.

## Self-Distribution Protocol

When a new machine comes online:

```
1. Clone plato-forge-daemon + plato-kernel
2. Pull live tiles from Oracle1's /export endpoints
3. Run forge-test.py to prove the pipeline works
4. Send I2I bottle: "ONLINE, hardware=X, VRAM=Ygb"
5. Fleet assigns training specialization
6. Start training on assigned data
7. Emit adapter checkpoints
8. Oracle1 validates (quality ≥ 0.94)
9. Fleet pulls and distributes
10. All nodes get smarter
```

Zero manual configuration. The protocol handles everything.

## Asymmetric Training

The key innovation: **different nodes train on different data → different adapters → shared cognition.**

| Node | Specialization | Training Data | Adapter |
|------|---------------|---------------|---------|
| FM (RTX 4050) | Kernel internals | plato-kernel traces | `kernel-adapter` |
| JC1 (Jetson) | Edge/CUDA | ct-lab experiments | `edge-adapter` |
| FM | Scoring/deadband | Fleet tile metadata | `scoring-adapter` |
| JC1 | Room dynamics | Zeroclaw traces | `room-adapter` |
| Cloud VM | Large-scale | Full fleet history | `fleet-adapter` |

When FM loads JC1's `edge-adapter`, FM gains intuition about constrained hardware — something FM never experienced. When JC1 loads FM's `kernel-adapter`, JC1 understands PLATO internals — something JC1 never built.

**That's flow-state-distributed thinking.**

## The Day/Night Cycle

Every node follows the same rhythm:

```
☀️ DAY (Inference Mode):
   - Load latest adapters
   - Run Neural Plato inference
   - Answer fleet queries
   - Generate training pairs from sessions
   - Push pairs to forge-buffer

🌙 NIGHT (Training Mode):
   - Swap to QLoRA training
   - Train on accumulated pairs
   - Emit adapter checkpoint every 100 steps
   - Push to Oracle1 for validation
   - Pull new validated adapters from fleet
```

## VM-Estate API

Nodes communicate via HTTP:

```
GET  /health              → node status, GPU info, VRAM free
GET  /adapters            → list of local adapters with quality scores
GET  /adapter/{id}        → download adapter binary
POST /adapter             → upload adapter for peer validation
GET  /export/tiles        → live tiles from local store
POST /export/pairs        → training pairs for peer
GET  /stats               → training progress, loss, step count
POST /train/start         → start training job
GET  /train/status        → current job progress
```

## Hardware Requirements

### Minimum (Jetson Orin Nano 8GB)
- LoRA training: 4.5GB VRAM
- Inference: 3.5GB VRAM (7B Q4)
- Storage: 10GB for repos + adapters

### Recommended (RTX 4050 6GB)
- LoRA training: 4.5GB VRAM
- Inference: 3.5GB VRAM
- Storage: 50GB for repos + adapters + training data

### Ideal (RTX 3080+ 10GB+)
- Full fine-tuning: 8GB+ VRAM
- Multiple adapters simultaneously
- Training + inference in parallel

## The Saltwater Principle, Evolved

JC1's original principle: "Every piece of knowledge in at least three repos."

VM-Estate evolution: **"Every thinking pattern in at least three adapters on at least three nodes."**

Kill any one node. Zero capability loss. The fleet thinks as one.

## Getting Started

1. Read the [Forge Onboarding Bottle](https://github.com/SuperInstance/forgemaster/blob/main/for-fleet/BOTTLE-FROM-FORGEMASTER-TO-JC1-2026-04-19-FORGE-ONBOARDING.md)
2. Clone `plato-forge-daemon`
3. Run `forge-test.py`
4. Watch loss converge
5. You're a plot in the VM-Estate.

## License

MIT — because intelligence should be free.

---

*"The code is the hull. The experience is the cargo. And the cargo is what makes the voyage worthwhile."* — JC1 🔧
