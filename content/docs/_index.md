---
date: '2026-10-29T10:31:30+01:00'
draft: false
title: 'Documentation'
cascade:
    type: docs
---

Ectopass is a tool detecting Spectre-V1 gadgets in source code.

{{< cards >}}
  {{< card link="installation" title="Installation" icon="arrow-circle-down" >}}
  {{< card link="using" title="Using Ectopass" icon="lightning-bolt" >}}
  {{< card link="configuration" title="Configuration" icon="adjustments" >}}
  {{< card link="roadmap" title="Roadmap" icon="film" >}}
{{< /cards >}}

## What is Spectre-V1?

Current processor optimizations such as branch prediction or speculation are essential for
performance but can break security by accidentally **leaking data**. See for example the [Spectre attack](https://spectreattack.com/).

An example of those is Spectre-V1 which is still hard to mitigate today and can have critical consequences by allowing
the attacker to leak any address is memory. Because of that all software are at risk and not only cryptography libraries
manipulating secrets.

{{< callout >}}
Ectopass helps by finding the code locations where those Spectre-V1 gadgets are, in a scalable way.
{{< /callout >}}

## How Ectopass works

Ectopass is implemented as an [LLVM](https://en.wikipedia.org/wiki/LLVM) pass (hence the name). It can be integrated with any codebase which can
be compiled to LLVM IR (C, C++, Rust, Swift, etc).

Ectopass performs a direct analysis of the Control Flow Graph of the program extended with speculative execution.

## Existing solutions

The existing solutions are either impractical (like changing the hardware) or do not scale for big codebases (like [SLH](https://llvm.org/docs/SpeculativeLoadHardening.html)).

Ectopass can help pinpoint the exact files where vulnerabilities can be found and limit the scope of SLH to those files.
Activating SLH to all files of a project (industry default) can be very time consuming.

Check out our benchmarks [here](../benchmarks)!

## Ectopass demo

On the [front page](..) you can try out Ectopass with a small C program. Ectopass will compile it to LLVM IR with:

```bash
clang-18 -emit-llvm -Og -g -S program.c
```
And then analyse it.
