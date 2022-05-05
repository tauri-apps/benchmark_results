# Benchmarks Results

[![Chat Server](https://img.shields.io/badge/chat-on%20discord-7289da.svg)](https://discord.gg/SpmNs4S)
[![devto](https://img.shields.io/badge/blog-dev.to-black.svg)](https://dev.to/tauri)
[![devto](https://img.shields.io/badge/documentation-tauri.studio-purple.svg)](https://tauri.studio/docs/getting-started/intro)
[![https://good-labs.github.io/greater-good-affirmation/assets/images/badge.svg](https://good-labs.github.io/greater-good-affirmation/assets/images/badge.svg)](https://good-labs.github.io/greater-good-affirmation)
[![support](https://img.shields.io/badge/sponsor-open%20collective-blue.svg)](https://opencollective.com/tauri)

All benchmarks run on Github Actions on `ubuntu-latest` matrix. We measure various metrics of the following applications:

| Tauri                 | Wry                   | Electron                 |
| :-------------------- | :-------------------- | :----------------------- |
| [tauri_cpu_intensive] | [wry_cpu_intensive]   | [electron_cpu_intensive] |
| [tauri_hello_world]   | [wry_hello_world]     | [electron_hello_world]   |
| [tauri_3mb_transfer]  | [wry_custom_protocol] | [electron_3mb_transfer]  |

[tauri_cpu_intensive]: https://github.com/tauri-apps/tauri/tree/dev/tooling/bench/tests/cpu_intensive
[tauri_hello_world]: https://github.com/tauri-apps/tauri/tree/dev/tooling/bench/tests/helloworld
[tauri_3mb_transfer]: https://github.com/tauri-apps/tauri/tree/dev/tooling/bench/tests/files_transfer
[wry_cpu_intensive]: https://github.com/tauri-apps/wry/tree/dev/bench/tests/src/cpu_intensive.rs
[wry_hello_world]: https://github.com/tauri-apps/wry/tree/dev/bench/tests/src/hello_world.rs
[wry_custom_protocol]: https://github.com/tauri-apps/wry/tree/dev/bench/tests/src/custom_protocol.rs
[electron_cpu_intensive]: https://github.com/tauri-apps/benchmark_electron/tree/dev/apps/cpu_intensive
[electron_hello_world]: https://github.com/tauri-apps/benchmark_electron/tree/dev/apps/hello_world
[electron_3mb_transfer]: https://github.com/tauri-apps/benchmark_electron/tree/dev/apps/file_transfer

---

### Data structure

```
interface ExecTimeData {
  mean: number;
  stddev: number;
  user: number;
  system: number;
  min: number;
  max: number;
}

interface BenchmarkData {
  created_at: string;
  sha1: string;
  exec_time: {
    [key: string]: ExecTimeData;
  };
  binary_size: {
    [key: string]: number;
  };
  thread_count: {
    [key: string]: number;
  };
  syscall_count: {
    [key: string]: number;
  };
  cargo_deps: {
    [key: string]: number;
  };
}
```

---

### Execution time

This shows how much time total it takes intialize the application and wait the `DOMContentLoaded` event. We use [hyperfine](https://github.com/sharkdp/hyperfine) under the hood and run 3 warm-up sequence then, we run 10 sequences to calculate the average execution time.

### Binary size

We track the size of various files here. All binary are compiled in release mode.

### Memory memory usage

We use `time -v` to get the max memory usage during execution. Smaller is better.

### Thread count

How many threads the application use. Smaller is better.

### Syscall count

How many total syscalls are performed when executing a given application. Smaller is better.

---

### CPU Intensive

The CPU intensive benchmark measures how much time it takes to calculate all the prime numbers under XXXX wihtout blocking the UI and reporting how many have been found so far using web workers.

### Hello World

This benchmark measures how long it takes to get an application fully started.

### Custom Protocol

Test WRY with a custom protocol. (local files)

---

### Acknowledgement

We would like to thank the authors and contributors to [deno](https://github.com/denoland/deno) for their groundbreaking work upon which the benchmarking system is not only based, but also leans heavily upon. Thankyou!!!
