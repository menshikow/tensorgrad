# Learning Zig

This is a learning path for someone coming from C++ that builds toward tensorgrad. Installed version: **Zig 0.16.0**.

## Resources

1. **Ziglings** (github.com/ratfactor/ziglings, now hosted on Codeberg) is a set of small broken programs you fix one at a time. It's the best hands-on start. Pick the branch or version that matches your compiler.
2. **The Language Reference** (ziglang.org/documentation/0.16.0/) is one long page that covers the whole language. Skim it once and come back to it as needed.
3. **The standard library source** is the real documentation. Yours is at `/opt/homebrew/Cellar/zig/0.16.0_1/lib/zig/std/`, and Zig developers read it all the time. `zig std` opens a browsable version.
4. **"Introduction to Zig"** by Pedro Duarte Faria is a free online book that's good for the bigger picture.
5. **Community:** Ziggit (ziggit.dev) is a forum where people answer beginner questions quickly.

> **A warning about versions:** Zig changes in breaking ways before 1.0. 0.15 rewrote I/O, and 0.16 changes it again. Many tutorials (including zig.guide) and LLM answers target older versions. If example code won't compile, check the version it was written for first.

## Concepts to focus on, coming from C++

- **Explicit allocators:** nothing allocates behind your back. You pass an `std.mem.Allocator` around. This matters for tensor storage.
- **Error unions and `try`:** these replace exceptions.
- **Slices vs. pointers:** `[]f64`, `[*]f64` and `*f64` are different types.
- **`comptime`:** this replaces templates. You'll use it to write one kernel for `f32` and `f64`.
- **`defer` / `errdefer`:** these replace RAII, since Zig has no destructors.
- **`@Vector`:** built-in SIMD, useful for fast kernels later.
- **`export fn` and the C ABI:** this is how Python will call your code.

## Practice path for tensorgrad

1. Work through Ziglings up to roughly the allocators and comptime exercises.
2. In `main.zig`, write `add` and `sum` for `[]f64` slices, with `test` blocks, and run `zig test main.zig`.
3. Write a `Tensor` struct with shape, strides and allocated storage, plus `init` and `deinit`.
4. Make one function generic over the element type with `comptime T: type`.
5. Add a `build.zig` that builds a shared library, then call it from Python with `ctypes`. That's milestone 1 of the roadmap.

Each step is small and touches only one or two new concepts.

## Useful commands

```sh
zig run main.zig      # compile and run
zig test main.zig     # run test blocks
zig fmt .             # format code
zig std               # browse standard library docs
```
