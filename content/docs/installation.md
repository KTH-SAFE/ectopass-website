---
date: '2026-10-29T10:31:30+01:00'
draft: false
title: 'Installation'
weight: 10
---

Ectopass will self-install the first time you run it. You don't need an internet connection.

## Requirements

Ectopass is currently only available on Linux on x86 processors.

Ectopass uses LLVM 18 so you would need to install it. On Ubuntu:

```
sudo apt install llvm-18 llvm-18-dev clang-18
```

## Installation folder

The first time it is run, Ectopass will install as follows in the `$HOME/.ectopass` folder:

{{< filetree/container >}}
  {{< filetree/folder name=".ectopass" >}}
    {{< filetree/file name="config.toml" >}}
    {{< filetree/file name="ectopass.so" >}}
    {{< filetree/folder name="bin" >}}
      {{< filetree/file name="ectopass" >}}
    {{< /filetree/folder >}}
    {{< filetree/folder name="results" >}}
    {{< /filetree/folder >}}
  {{< /filetree/folder >}}
{{< /filetree/container >}}

Add `$HOME/.ectopass/bin` to your `PATH` to be able to use `ectopass`.
