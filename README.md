# narrowc

A lightweight compiler that turns a narrow, explicit subset of Python into C. Anything outside that subset falls back to running as normal Python — nothing silently breaks.

## Spec

See [`python-to-c-compiler-spec-1.docx`](python-to-c-compiler-spec-1.docx) for the full supported / not-supported breakdown.

## Getting started

```bash
unzip narrowc.zip
```

## Build & run

```bash
 gcc -std=c11 -Wall -Wextra -O2 ast_walker.c -o ast_walker \
       $(python3-config --embed --cflags --ldflags) -lm
./ast_walker --check yourscript.py      # check if it's in the supported subset
./ast_walker yourscript.py output.c     # compile to C
gcc -std=c11 -O2 output.c -o output -lm # compile the generated C
./output
```

## Benchmark

A benchmark script is included to compare compiled vs. interpreted speed.

> **Note:** The raw benchmark speedup is not accurate as-is — GCC's `-O2` can fold simple accumulator-style math into a closed-form result, which inflates the number. The real, measured speedup on a genuine compute-bound loop (built with `-O0`) is closer to **35x**.

## License

MIT
