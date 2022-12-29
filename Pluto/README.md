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

