# OpenCL-Benchmark

A small [OpenCL](https://github.com/ProjectPhysX/OpenCL-Wrapper "OpenCL-Wrapper") benchmark program to measure peak GPU/CPU performance.

Works with any GPU in Windows, Linux, macOS and Android.



## Measurements
- compute performance (`FP64` (scalar), `FP32` (scalar), `FP16` (half2), `INT64` (scalar), `INT32` (scalar), `INT16` (short2), `INT8` (dp4a))
  - closest possible fraction/multiplicator of `measured compute performance` divided by `reported theoretical FP32 performance` is shown in `(round brackets)`
    - for example when OpenCL reports `19.492` TFLOPs/s theoretical FP32, and the benchmark measures `9.512` TFLOPs/s for FP64, the ratio of `(measured FP64)/(theoretical FP32) = 9.512/19.492 = 1/2.05` is rounded to the next possible value of `1/2` and reported as such
    - these ratios for any GPU/CPU architecture can only be either `1/64`, `1/32`, `1/24`, `1/16`, `1/12`, `1/8`, `1/4`, `1/3`, `1/2`, `2/3`, `1x`, `2x`, `4x`, `8x`, `16x`, `32x`, `64x`, and nothing in between
- memory bandwidth (`coalesced`/`misaligned` `read`/`write`)
- PCIe bandwidth (`send`/`receive`/`bidirectional`)
  - PCIe Gen is estimated based on measured PCIe bandwidth and assumed x16 link width



## How to use?

### Windows
- Download and install [Visual Studio Community](https://visualstudio.microsoft.com/de/vs/community/). In Visual Studio Installer, add:
  - Desktop development with C++
  - MSVC v142
  - Windows 10 SDK
- Open [`OpenCL-Benchmark.sln`](OpenCL-Benchmark.sln) in [Visual Studio Community](https://visualstudio.microsoft.com/de/vs/community/).
- Compile and run by clicking the <kbd>► Local Windows Debugger</kbd> button.
- To run outside of [Visual Studio Community](https://visualstudio.microsoft.com/de/vs/community/), open Windows CMD in the `OpenCL-Benchmark` folder (type `cmd` in File Explorer in the directory field and press <kbd>Enter</kbd>), then run
  ```
  OpenCL-Benchmark.exe
  ```

### Linux / macOS / Android
- Download, compile and run:
  ```
  git clone https://github.com/ProjectPhysX/OpenCL-Benchmark.git
  cd OpenCL-Benchmark
  chmod +x make.sh
  ./make.sh
  ```
- Run
  ```
  bin/OpenCL-Benchmark
  ```
- Compile and run using cmake
  ```
  cd OpenCL-Benchmark
  cmake -S . -B build
  cmake --build build -j4
  build/OpenCL-Benchmark
  ```

### Run only for a specified list of devices
- call `bin\OpenCL-Benchmark.exe 0 2 5` (Windows) or `bin/OpenCL-Benchmark 0 2 5` (Linux/macOS) with the number(s) being the device IDs to be benchmarked



## Examples
```
|----------------.------------------------------------------------------------|
| Device ID      | 0                                                          |
| Device Name    | NVIDIA H100 80GB HBM3                                      |
| Device Vendor  | NVIDIA Corporation                                         |
| Device Driver  | 565.57.01 (Linux)                                          |
| OpenCL Version | OpenCL C 3.0                                               |
| Compute Units  | 132 at 1980 MHz (16896 cores, 66.908 TFLOPs/s)             |
| Memory, Cache  | 81105 MB VRAM, 4224 KB global / 48 KB local                |
| Buffer Limits  | 20276 MB global, 64 KB constant                            |
|----------------'------------------------------------------------------------|
| Info: OpenCL C code successfully compiled.                                  |
| FP64  compute                                        31.184 TFLOPs/s (1/2 ) |
| FP32  compute                                        62.908 TFLOPs/s ( 1x ) |
| FP16  compute                                       123.749 TFLOPs/s ( 2x ) |
| INT64 compute                                         3.227  TIOPs/s (1/24) |
| INT32 compute                                        32.946  TIOPs/s (1/2 ) |
| INT16 compute                                        30.901  TIOPs/s (1/2 ) |
| INT8  compute                                       103.204  TIOPs/s ( 2x ) |
| Memory Bandwidth ( coalesced read      )                       3025.53 GB/s |
| Memory Bandwidth ( coalesced      write)                       3055.98 GB/s |
| Memory Bandwidth (misaligned read      )                       2102.44 GB/s |
| Memory Bandwidth (misaligned      write)                        314.25 GB/s |
| PCIe   Bandwidth (send                 )                         10.53 GB/s |
| PCIe   Bandwidth (   receive           )                         11.47 GB/s |
| PCIe   Bandwidth (        bidirectional)            (Gen4 x16)   10.91 GB/s |
|-----------------------------------------------------------------------------|
```
```
|----------------.------------------------------------------------------------|
| Device ID      | 0                                                          |
| Device Name    | AMD Instinct MI300X                                        |
| Device Vendor  | Advanced Micro Devices, Inc.                               |
| Device Driver  | 3635.0 (HSA1.1,LC) (Linux)                                 |
| OpenCL Version | OpenCL C 2.0                                               |
| Compute Units  | 304 at 2100 MHz (19456 cores, 81.715 TFLOPs/s)             |
| Memory, Cache  | 196592 MB VRAM, 32 KB global / 64 KB local                 |
| Buffer Limits  | 196592 MB global, 201310208 KB constant                    |
|----------------'------------------------------------------------------------|
| Info: OpenCL C code successfully compiled.                                  |
| FP64  compute                                        54.944 TFLOPs/s (2/3 ) |
| FP32  compute                                       130.000 TFLOPs/s ( 2x ) |
| FP16  compute                                       141.320 TFLOPs/s ( 2x ) |
| INT64 compute                                         3.666  TIOPs/s (1/24) |
| INT32 compute                                        47.736  TIOPs/s (2/3 ) |
| INT16 compute                                        69.022  TIOPs/s ( 1x ) |
| INT8  compute                                       106.178  TIOPs/s ( 1x ) |
| Memory Bandwidth ( coalesced read      )                       3756.64 GB/s |
| Memory Bandwidth ( coalesced      write)                       4686.31 GB/s |
| Memory Bandwidth (misaligned read      )                       3881.24 GB/s |
| Memory Bandwidth (misaligned      write)                       2491.25 GB/s |
| PCIe   Bandwidth (send                 )                         54.57 GB/s |
| PCIe   Bandwidth (   receive           )                         55.79 GB/s |
| PCIe   Bandwidth (        bidirectional)            (Gen4 x16)   55.21 GB/s |
|-----------------------------------------------------------------------------|
```
```
|----------------.------------------------------------------------------------|
| Device ID      | 0                                                          |
| Device Name    | Intel(R) Arc(TM) B580 Graphics                             |
| Device Vendor  | Intel(R) Corporation                                       |
| Device Driver  | 32.0.101.6559 (Windows)                                    |
| OpenCL Version | OpenCL C 3.0                                               |
| Compute Units  | 160 at 2850 MHz (2560 cores, 14.592 TFLOPs/s)              |
| Memory, Cache  | 12187 MB VRAM, 18432 KB global / 128 KB local              |
| Buffer Limits  | 11944 MB global, 12230900 KB constant                      |
|----------------'------------------------------------------------------------|
| Info: OpenCL C code successfully compiled.                                  |
| FP64  compute                                         0.896 TFLOPs/s (1/16) |
| FP32  compute                                        14.249 TFLOPs/s ( 1x ) |
| FP16  compute                                        26.547 TFLOPs/s ( 2x ) |
| INT64 compute                                         0.636  TIOPs/s (1/24) |
| INT32 compute                                         4.556  TIOPs/s (1/3 ) |
| INT16 compute                                        37.082  TIOPs/s ( 2x ) |
| INT8  compute                                        48.668  TIOPs/s ( 4x ) |
| Memory Bandwidth ( coalesced read      )                        574.09 GB/s |
| Memory Bandwidth ( coalesced      write)                        468.07 GB/s |
| Memory Bandwidth (misaligned read      )                        796.23 GB/s |
| Memory Bandwidth (misaligned      write)                        383.15 GB/s |
| PCIe   Bandwidth (send                 )                          4.99 GB/s |
| PCIe   Bandwidth (   receive           )                          4.87 GB/s |
| PCIe   Bandwidth (        bidirectional)            (Gen3 x16)    5.11 GB/s |
|-----------------------------------------------------------------------------|
|----------------.------------------------------------------------------------|
```
```
|----------------.------------------------------------------------------------|
| Device ID      | 0                                                          |
| Device Name    | AMD EPYC 9554 64-Core Processor                            |
| Device Vendor  | Intel(R) Corporation                                       |
| Device Driver  | 2024.18.10.0.08_160000 (Linux)                             |
| OpenCL Version | OpenCL C 3.0                                               |
| Compute Units  | 128 at 0 MHz (64 cores, 0.000 TFLOPs/s)                    |
| Memory, Cache  | 386363 MB RAM, 1024 KB global / 256 KB local               |
| Buffer Limits  | 386363 MB global, 128 KB constant                          |
|----------------'------------------------------------------------------------|
| Info: OpenCL C code successfully compiled.                                  |
| FP64  compute                                         3.739 TFLOPs/s (1/64) |
| FP32  compute                                         3.842 TFLOPs/s (1/64) |
| FP16  compute                                         0.863 TFLOPs/s (1/64) |
| INT64 compute                                         1.506  TIOPs/s (1/64) |
| INT32 compute                                         4.240  TIOPs/s (1/64) |
| INT16 compute                                         8.592  TIOPs/s (1/64) |
| INT8  compute                                         2.774  TIOPs/s (1/64) |
| Memory Bandwidth ( coalesced read      )                        391.09 GB/s |
| Memory Bandwidth ( coalesced      write)                        167.26 GB/s |
| Memory Bandwidth (misaligned read      )                        248.65 GB/s |
| Memory Bandwidth (misaligned      write)                        156.18 GB/s |
|-----------------------------------------------------------------------------|
```
```
|----------------.------------------------------------------------------------|
| Device ID      | 1                                                          |
| Device Name    | Intel(R) UHD Graphics 630                                  |
| Device Vendor  | Intel(R) Corporation                                       |
| Device Driver  | 31.0.101.2130 (Windows)                                    |
| OpenCL Version | OpenCL C 3.0                                               |
| Compute Units  | 24 at 1200 MHz (192 cores, 0.461 TFLOPs/s)                 |
| Memory, Cache  | 6500 MB RAM, 768 KB global / 64 KB local                   |
| Buffer Limits  | 3250 MB global, 3328048 KB constant                        |
|----------------'------------------------------------------------------------|
| Info: OpenCL C code successfully compiled.                                  |
| FP64  compute                                         0.112 TFLOPs/s (1/4 ) |
| FP32  compute                                         0.437 TFLOPs/s ( 1x ) |
| FP16  compute                                         0.801 TFLOPs/s ( 2x ) |
| INT64 compute                                         0.016  TIOPs/s (1/32) |
| INT32 compute                                         0.149  TIOPs/s (1/3 ) |
| INT16 compute                                         0.863  TIOPs/s ( 2x ) |
| INT8  compute                                         0.213  TIOPs/s (1/2 ) |
| Memory Bandwidth ( coalesced read      )                         20.98 GB/s |
| Memory Bandwidth ( coalesced      write)                         25.18 GB/s |
| Memory Bandwidth (misaligned read      )                         35.16 GB/s |
| Memory Bandwidth (misaligned      write)                         16.18 GB/s |
|-----------------------------------------------------------------------------|
```
```
|----------------.------------------------------------------------------------|
| Device ID      | 2                                                          |
| Device Name    | Intel(R) Core(TM) i7-8700K CPU @ 3.70GHz                   |
| Device Vendor  | Intel(R) Corporation                                       |
| Device Driver  | 2024.17.3.0.08_160000 (Windows)                            |
| OpenCL Version | OpenCL C 3.0                                               |
| Compute Units  | 12 at 3700 MHz (6 cores, 0.710 TFLOPs/s)                   |
| Memory, Cache  | 16250 MB RAM, 256 KB global / 32 KB local                  |
| Buffer Limits  | 16250 MB global, 128 KB constant                           |
|----------------'------------------------------------------------------------|
| Info: OpenCL C code successfully compiled.                                  |
| FP64  compute                                         0.151 TFLOPs/s (1/4 ) |
| FP32  compute                                         0.158 TFLOPs/s (1/4 ) |
| FP16  compute                                          not supported        |
| INT64 compute                                         0.042  TIOPs/s (1/16) |
| INT32 compute                                         0.063  TIOPs/s (1/12) |
| INT16 compute                                         0.224  TIOPs/s (1/3 ) |
| INT8  compute                                         0.059  TIOPs/s (1/12) |
| Memory Bandwidth ( coalesced read      )                         16.92 GB/s |
| Memory Bandwidth ( coalesced      write)                          8.08 GB/s |
| Memory Bandwidth (misaligned read      )                         40.02 GB/s |
| Memory Bandwidth (misaligned      write)                         13.69 GB/s |
|-----------------------------------------------------------------------------|
```