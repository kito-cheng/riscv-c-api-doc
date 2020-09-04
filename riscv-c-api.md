# RISC-V C API Specification

This file contains the RISC-V additions to the standard C APIs.  It
merges together the compiler command-line API, the preprocessor API, and
the C language extensions (function attributes and intrinsic functions).

## Copyright and license information

 &copy; 2018 Palmer Dabbelt <palmer@sifive.com>

 &copy; 2018 SiFive, Inc

It is licensed under the Creative Commons Attribution 4.0 International
License (CC-BY 4.0). The full license text is available at
https://creativecommons.org/licenses/by/4.0/.

## Compiler Command-Line Arguments

* `-mabi=ABI`
* `-march=ISA`
* `-mtune=MICRO_ARCHITECTURE`
* `-mplt` `-mno-plt`
* `-mcmodel=CODE_MODEL`
* `-mstrict-align` '-mno-strict-align`
* `-mfdiv` `-mno-fdiv`
* `-mdiv` `-mno-div`
* `-mpreferred-stack-boundary=N`
* `-msmall-data-limit=N`
* `-mexplicit-relocs` '-mno-explicit-relocs`
* `-mrelax` `-mno-relax`
* `-msave-restore` `-mno-save-restore`
* `-mbranch-cost=N`

## Preprocessor Definitions

| Name                | Value | When defined                  |
| ------------------- | ----- | ----------------------------- |
| __riscv             | 1     | Always defined.               |
| __riscv_xlen        | <ul><li>32 for rv32</li><li>64 for rv64</li><li>128 for rv128</ul> | Always defined.             |
| __riscv_flen        | <ul><li>32 if the F extension is available **or**</li><li>64 if `D` extension available **or**</li><li>128 if `Q` extension available</li></ul> | `F` extension is available. |
| __riscv_32e         | 1     | `E` extension is available.   |
| __riscv_atomic      | 1     | `A` extension is available.   |
| __riscv_compressed  | 1     | `C` extension is available.   |
| __riscv_mul         | 1     | `M` extension is available.   |
| __riscv_div         | 1     | `M` extension is available and `-mno-div` is not given.*[1]    |
| __riscv_muldiv      | 1     | `M` extension is available and `-mno-div` is not given.*[1]    |
| __riscv_fdiv        | 1     | `F` extension is available and `-mno-fdiv` is not given.*[1]   |
| __riscv_fsqrt       | 1     | `F` extension is available and `-mno-fdiv` is not given.*[1]   |
| __riscv_vector      | 1     | `V` extension is available.   |
| __riscv_bitmanip    | 1     | `B` extension is available.   |
| __riscv_zfh         | 1     | `Zfh` extension is available. |

*[1] Not all compiler provide `-mno-div` and `-mno-fdiv` option.

### ABI Related Preprocessor Definitions

| Name                     | Value | When defined                  |
| ------------------------ | ----- | ----------------------------- |
| __riscv_abi_rve          | 1     | Defined if using `ilp32e` ABI |
| __riscv_float_abi_soft   | 1     | Defined if using `ilp32`, `ilp32e` or `lp64` ABI. |
| __riscv_float_abi_single | 1     | Defined if using `ilp32f` or `lp64f` ABI. |
| __riscv_float_abi_double | 1     | Defined if using `ilp32d` or `lp64d` ABI. |
| __riscv_float_abi_quad   | 1     | Defined if using `ilp32q` or `lp64q` ABI. |

### Code Model Related Preprocessor Definitions

| Name                  | Value    | When defined                          |
| --------------------- | -------- | ------------------------------------- |
| __riscv_cmodel_medlow | 1        | Defined if using `medlow` code model. |
| __riscv_cmodel_medany | 1        | Defined if using `medany` code model. |

### Deprecated Preprocessor Definitions

| Name                  | Value    | When defined                          | Alternative |
| --------------------- | -------- | ------------------------------------- | ----------- |
| __riscv_cmodel_pic    | 1        | GCC will defined that when program compile with -fPIC, -fpic, -fPIE or -fpie. | `__PIC__` or `__PIE__` |

## Function Attributes

* `__attribute__((naked))`
* `__attribute__((interrupt))`
* `__attribute__((interrupt("user")))`
* `__attribute__((interrupt("supervisor")))`
* `__attribute__((interrupt("machine")))`

## Intrinsic Functions

Do we really have none of these?  I can't figure out
`gcc/gcc/config/riscv/riscv-builtins.c`...
