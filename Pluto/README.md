# Pluto-Obfuscator

- [Homepage](https://github.com/bluesadi/Pluto-Obfuscator)

## Version

This is based off current HEAD ``3c332857429162015aef94d875eafc95a60112f8``

## Source Code Structure

- [Tests](https://github.com/bluesadi/Pluto-Obfuscator/tree/3c332857429162015aef94d875eafc95a60112f8/test)

gitsubmodule is a thing

- [exhaustive_tests-tests_exhaustive-0fa0cf44.o.tmp](https://github.com/bluesadi/Pluto-Obfuscator/blob/3c332857429162015aef94d875eafc95a60112f8/test/secp256k1/src/exhaustive_tests-tests_exhaustive-0fa0cf44.o.tmp)

gitignore is also a thing

- [llvm](https://github.com/bluesadi/Pluto-Obfuscator/blob/main/llvm/)

LLVM has had proper PassPlugin support since 10.x, there is no need to ship the full LLVM source anymore.

## Test Selection
``secp256k1`` is pure C, and ``aes`` is literally C written in a C++ source, there is no way these cases are enough to test the vast amount of compiler bugs

## Transform Implementations
### BCF
#### InlineAsm
[InlineAsm](https://llvm.org/docs/LangRef.html#inline-assembler-expressions) is only valid as an operand to ``CallInst`` or ``InvokeInst``, there is no need to filter all operands of all Instructions.

Plus, if ``InlineAsm`` is written with proper constraints, BCF won't break them, if not, then this is an user error. BCF as a pass shouldn't be filtering out functions containing them.

#### Opaque Predicate

MBA should be used here directly, instead of relying on another standalone pass (which is also retarded, which we'll elaborate later.)

### GlobalEncryption

- Decrypt all GlobalVariables in constructor provides next to no protection at all.
- Module Constructors are not always the first user-related code to run, Objective-C runtime initialization takes place before the ctor, which results in Objective-C constructed from obfuscated strings, hence completely broke the program.

### RandomControlFlow

Loading from an unitialized memory (the alloca without store), is an UB and will trigger bugs like [54545](https://github.com/llvm/llvm-project/issues/54545) if no extra steps are done to take care of it. I can now safely say no such step is done properly

### Substitution

The rules are way too naive to an extent that it's laughable

### MBA
The input variables are implemented as a load from GV, which is trivially foldable by IDA, making it next to useless

### VariableSubstituion

Combined all the weakness from Sub and MBA

