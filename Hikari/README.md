# Hikari
We'll be using [NeHyci's fork](https://github.com/NeHyci/Hanabi) as our evaluation target

## Version
This is based off current HEAD ``c11086f461d62974d3e8b01bb39af2608284430c``

## Source Code Structure

LLVM has had proper PassPlugin support since 10.x, there is no need to ship the full LLVM source anymore.

## Test Selection
N/A

## Transform Implementations
### AnitDebugging
There are multiple more obscure and API-less implementation possible, this is bad.

### BogusControlFlow
Multiple creative changes could be observed, my only nitpick is the OpaquePredicate generation.
Suggestion: See Pluto Analysis

### ControlFlowFlattening
- The algorithm is known to have issues with SEH semantics.
- ValueEscape Analysis is broken and will lower more Instructions than needed

### Substitution
Need more patterns
