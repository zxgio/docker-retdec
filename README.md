# docker-retdec

[![CircleCI](https://circleci.com/gh/blacktop/docker-retdec.png?style=shield)](https://circleci.com/gh/blacktop/docker-retdec) [![License](http://img.shields.io/:license-mit-blue.svg)](http://doge.mit-license.org) [![Docker Stars](https://img.shields.io/docker/stars/blacktop/retdec.svg)](https://hub.docker.com/r/blacktop/retdec/) [![Docker Pulls](https://img.shields.io/docker/pulls/blacktop/retdec.svg)](https://hub.docker.com/r/blacktop/retdec/) [![Docker Image](https://img.shields.io/badge/docker%20image-4.29GB-blue.svg)](https://hub.docker.com/r/blacktop/retdec/)

This repository contains a **Dockerfile** of [RetDec](https://github.com/avast-tl/retdec) **blacktop/retdec**.

---

## Dependencies

- [ubuntu:bionic](https://hub.docker.com/r/_/ubuntu/)

## Image Tags

```bash
$ docker images

REPOSITORY          TAG        SIZE       TAR
blacktop/retdec     latest     4.29GB     369MB
blacktop/retdec     3.2        4.29GB     369MB
```

> **NOTE:** why is this image so large??? :neutral_face:

```bash
retdec@17b1596c8f0c:/$ du -sh /usr/share/retdec/

"3.9G"    /usr/share/retdec/
```

## Installation

1.  Install [Docker](https://docs.docker.com).
2.  Download [trusted build](https://hub.docker.com/r/blacktop/retdec/) from public [Docker Registry](https://hub.docker.com): `docker pull blacktop/retdec`

## Getting Started

```bash
$ docker run --rm -v `pwd`:/samples blacktop/retdec
```

```
Decompiles the given file into the selected target high-level language.

Usage:
    /usr/share/retdec/bin/decompile.sh [ options ] file

Options:
    -a name,   --arch name                            Specify target architecture [mips|pic32|arm|thumb|powerpc|x86] (default: x86).
    -e name,   --endian name                          Specify target endianness [little|big] (default: little). Not all combinations are supported.
    -f name,   --format name                          Specify object file format [elf|pe|ihex|macho] (default: pe).
    -h,        --help                                 Print this help message.
    -k         --keep-unreachable-funcs               Keep functions that are unreachable from the main function.
    -l string, --target-language string               Target high-level language [c|py] (default: c).
    -m name,   --mode name                            Force the type of decompilation mode [bin|ll|raw] (default: ll if input's suffix is '.ll', bin otherwise).
    -o file,   --output file                          Output file (default: file.ext).
    -p file,   --pdb file                             File with PDB debug information.
               --ar-index name                        Pick file from archive for decompilation by its zero-based index.
               --ar-name string                       Pick file from archive for decompilation by its name.
               --backend-aggressive-opts              Enables aggressive optimizations.
               --backend-arithm-expr-evaluator string Name of the used evaluator of arithmetical expressions (default: c).
               --backend-call-info-obtainer string    Name of the obtainer of information about function calls (default: optim).
               --backend-cfg-test                     Unifies the labels of all nodes in the emitted CFG (this has to be used in tests).
               --backend-disabled-opts list           Prevents the optimizations from the given comma-separated list of optimizations to be run.
               --backend-emit-cfg                     Emits a CFG for each function in the backend IR (in the .dot format).
               --backend-emit-cg                      Emits a CG for the decompiled module in the backend IR (in the .dot format).
               --backend-cg-conversion string         Should the CG from the backend be converted automatically into the desired format? [auto|manual] (default: auto).
               --backend-cfg-conversion string        Should CFGs from the backend be converted automatically into the desired format? [auto|manual] (default: auto).
               --backend-enabled-opts list            Runs only the optimizations from the given comma-separated list of optimizations.
               --backend-find-patterns list           Runs the finders of patterns specified in the given comma-separated list (use 'all' to run them all).
               --backend-force-module-name string     Overwrites the module name that was detected/generated by the front-end.
               --backend-keep-all-brackets            Keeps all brackets in the generated code.
               --backend-keep-library-funcs           Keep functions from standard libraries.
               --backend-llvmir2bir-converter string  Name of the converter from LLVM IR to BIR (default: orig).
               --backend-no-compound-operators        Do not emit compound operators (like +=) instead of assignments.
               --backend-no-debug                     Disables the emission of debug messages, such as phases.
               --backend-no-debug-comments            Disables the emission of debug comments in the generated code.
               --backend-no-opts                      Disables backend optimizations.
               --backend-no-symbolic-names            Disables the conversion of constant arguments to their symbolic names.
               --backend-no-time-varying-info         Do not emit time-varying information, like dates.
               --backend-no-var-renaming              Disables renaming of variables in the backend.
               --backend-semantics                    A comma-separated list of the used semantics.
               --backend-strict-fpu-semantics         Forces strict FPU semantics to be used.
               --backend-var-renamer string           Used renamer of variables [address|hungarian|readable|simple|unified] (default: readable).
               --cleanup                              Removes temporary files created during the decompilation.
               --color-for-ida                        Put IDA Pro color tags to output C file.
               --config name                          Specify JSON decompilation configuration file.
               --no-config                            State explicitly that config file is not to be used.
               --fileinfo-verbose                     Print all detected information about input file.
               --fileinfo-use-all-external-patterns   Use all detection rules from external YARA databases.
               --graph-format name                    Specify format of a all generated graphs (e.g. CG, CFG) [pdf|png|svg] (default: png).
               --raw-entry-point addr                 Entry point address used for raw binary (default: architecture dependent).
               --raw-section-vma addr                 Virtual address where section created from the raw binary will be placed (default: architecture dependent).
               --select-decode-only                   Decode only selected parts (functions/ranges). Faster decompilation, but worse results.
               --select-functions list                Specify a comma separated list of functions to decompile (example: fnc1,fnc2,fnc3).
               --select-ranges list                   Specify a comma separated list of ranges to decompile (example: 0x100-0x200,0x300-0x400,0x500-0x600).
               --stop-after tool                      Stop the decompilation after the given tool (supported tools: fileinfo, unpacker, bin2llvmir, llvmir2hll).
               --static-code-sigfile path             Adds additional signature file for static code detection.
               --static-code-archive path             Adds additional signature file for static code detection from given archive.
               --no-default-static-signatures         No default signatures for statically linked code analysis are loaded (options static-code-sigfile/archive are still available).
```

### Decompile some [malware](https://www.virustotal.com/#/file/befb88b89c2eb401900a68e9f5b78764203f2b48264fcc3f7121bf04a57fd408/behavior)

```bash
$ docker run --rm -v `pwd`:/samples blacktop/retdec FILE
```

#### To see an example output C file look [here](https://github.com/blacktop/docker-retdec/blob/master/samples/befb88b89c2eb401900a68e9f5b78764203f2b48264fcc3f7121bf04a57fd408.c)

## Issues

Find a bug? Want more features? Find something missing in the documentation? Let me know! Please don't hesitate to [file an issue](https://github.com/blacktop/docker-retdec/issues/new).

## License

MIT Copyright (c) 2018 **blacktop**
