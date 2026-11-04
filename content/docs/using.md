---
date: '2026-10-29T10:31:30+01:00'
draft: false
title: 'Using Ectopass'
weight: 20
---

Once Ectopass is [installed](../installation), you are ready to run it!

For a quick test, save the demo C program on the home page in a `program.c` file and run `ectopass program.c`.
You should get the same output!

If you look in the `$HOME/.ectopass/results` folder, you should be able to see two new files:
* `out.ll`: the LLVM IR generated from this C program
* `result.json`: the machine-readable output format of Ectopass

The location of where the output results are generated and their format can be changed in the
[configuration](../configuration) file.

## Output format

Ectopass emits one JSON file per input analysed in the results directory.
It follows the [`PublishDiagnosticsParams`](https://microsoft.github.io/language-server-protocol/specifications/lsp/3.17/specification/#publishDiagnosticsParams) interface from the Language Server Protocol.
At the end of the analysis, Ectopass reads this file and pretty prints its content on the command-line.

See the different options with `ectopass --help` to modify the CLI output.

## Integration in larger projects

Ectopass can only directly be used with C files if they are self-contained. Typical projects will be
composed of a lot of files with different dependencies and its own build system. Each file might have
specific build options too.

Ectopass can instead be called with the LLVM IR files as input, generated with the same build options
as the object files.

{{< callout type="warning" >}}
 **Debug information are needed** in order to show code locations.
{{< /callout >}}

You can either:
* Modify your existing build system to add a rule generating LLVM IR.
* For C projects, replace your compiler with an LLVM IR shim compiler.
The shim will generate the LLVM IR file using `clang-18` and the same
build options as the original call. See below for an example.

{{< details title="LLVM IR shim compiler" closed="true" >}}

```python
#!/usr/bin/env python3

# Compilation shim using clang-18 to also generate LLVM IR with the same compilation flags.

import sys
import subprocess
import copy

def main():
    generate_ir_args = copy.deepcopy(sys.argv[1:])
    #print(" ".join(generate_ir_args))

    # Check if we are compiling a C file. We don't want to run
    # Ectopass for assembly files.  The input file is provided as a
    # positional argument, which is not necessarily the last
    # argument. It's not trivial to identify the positional arguments
    # because it requires a complete knowledge of how the compiler
    # parses all of its arguments. Having a conservative approach by
    # checking if any of the arguments ends with '.s' or '.S'.
    if "-o" in generate_ir_args \
            and "-c" in generate_ir_args \
            and "-S" not in generate_ir_args \
            and not any(arg.lower().endswith(".s") for arg in generate_ir_args):
        # Modify the arguments to generate LLVM IR with debug info instead.
        # Replace the ".o" output file (after the "-o" option) to ".o.ll".
        target_index = generate_ir_args.index("-o") + 1
        object_file = generate_ir_args[target_index]
        generate_ir_args[target_index] += ".ll"
        generate_ir_args += ["-emit-llvm"]
        generate_ir_args += ["-g"]
        generate_ir_args += ["-S"]

        # Generate IR
        cmd = subprocess.run(
            ["clang-18"] + generate_ir_args,
            stdin=sys.stdin,
            stdout=sys.stdout,
            stderr=sys.stderr,
            check=True
        )
        #print(" ".join(cmd.args))

    # Forward original call using clang-18
    cmd = subprocess.run(
        ["clang-18"] + sys.argv[1:],
        stdin=sys.stdin,
        stdout=sys.stdout,
        stderr=sys.stderr,
        check=True
    )
    #print(" ".join(cmd.args))

if __name__ == "__main__":
    main()
```

{{< /details >}}

Once you have the LLVM IR file, you can just run `ectopass` on them!

