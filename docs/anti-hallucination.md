# Anti-Hallucination Training Guide

## The Problem
Weak LLMs (sub-130B parameters) are prone to:
- Inventing plausible-looking numbers when tools fail
- Mixing data from different sources/contexts
- Repeating stale conclusions from conversation history
- Substituting related-but-wrong answers for unavailable capabilities
- Continuing to explore after sufficient data is collected

## The Solution: Layered Rules

### Layer 1: System Prompt (SOUL.md)
Core thinking discipline embedded in agent identity. These are always present.

### Layer 2: Skill Files (tool-discipline, tool-use-patterns)
Domain-specific rules loaded when relevant. Contain real examples.

### Layer 3: Test Harness (36-test suite)
Continuous validation that rules are being followed. Tests cover:
- Correct tool invocation (not from memory)
- Error handling (no fabrication)
- Safety tiers (refuse destructive without confirmation)
- Focus (answer only what was asked)
- Memory (recall from correct source)

## Training Loop

```
1. Run 36-test baseline → identify failures
2. Classify each failure:
   - Missing instruction? → add rule to SOUL.md or skill
   - Missing example? → add pattern to tool-use-patterns
   - Model limitation? → add retry-guard or structural constraint
3. Fix and re-run affected tests only
4. Full suite re-validation after each major change
5. Stop when 100% pass rate achieved
```

## Real Failure Examples (Anonymized)

### Failure: Fabricated pairing
**Question**: "Is there an IP conflict on .52?"
**Wrong answer**: Glued a MAC from VLAN-A logs with an IP from VLAN-B logs,
claiming they were a "conflict pair."
**Root cause**: No rule about cross-context data mixing.
**Fix**: Rule 6 — "Don't glue facts from different contexts without verifying
they share the same VLAN/gateway/time window."

### Failure: Recycled stale conclusion
**Question**: (repeated) "Is DHCP working?"
**Wrong answer**: Repeated "DHCP is broken" from 2 hours ago, ignoring
that it was fixed in between.
**Root cause**: Treating conversation history as ground truth.
**Fix**: Rule 5 — "Old conclusions are NOT facts. RE-VERIFY with tools NOW."

### Failure: Task substitution
**Question**: "Read the network logs"
**Wrong answer**: Dumped 2 screens of network configuration instead.
**Root cause**: No rule about capability gaps.
**Fix**: Rule 4 — "If capability doesn't exist, say exactly that."
