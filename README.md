# Adaptive Spatial Indexing

**Online adaptive spatial index selection for fixed-radius neighbor search in dynamic particle systems.**

[Русская версия](README_RU.md)

`adaptive-spatial-indexing` is a research-oriented C++20 project for the comparative study of spatial indexing methods under dynamic particle workloads.

This repository is **not** intended to demonstrate one preferred spatial data structure. It is designed as an experimental framework for implementing, validating, benchmarking, and comparing several neighbor-search approaches under changing distributions, motion patterns, and hardware configurations.

## Problem

A dynamic particle system contains points whose positions change over time. At every simulation step, the system must find all particle pairs whose distance does not exceed a fixed interaction radius.

A brute-force search checks every pair and provides a simple correctness reference, but its quadratic cost makes it unsuitable for large systems. Spatial indices reduce the number of candidate pairs, although their performance depends strongly on the workload.

The project studies the trade-off between:

- **query performance** — latency, throughput, and candidate-pair count;
- **update cost** — construction, reuse, refit, and rebuild overhead;
- **memory usage** — index storage and neighbor-list representation;
- **robustness** — behavior across uniform, sparse, clustered, and changing workloads.

## Research question

> Can an online policy select a spatial index and update strategy that approaches the performance of the best specialized method across changing dynamic workloads?

The selector will eventually use inexpensive workload characteristics such as particle count, density variance, cell occupancy, displacement, radius, and previous timing measurements.

## Approaches under study

| Family | Planned approaches | Main purpose |
|---|---|---|
| Correctness baseline | brute-force pair search | produce exact reference neighbor pairs |
| Regular grids | dense uniform grid | exploit uniform spatial locality |
| Sparse grids | hashed grid | avoid storage for empty regions |
| Spatial ordering | Morton/Z-order sorting and contiguous cell ranges | improve locality and reduce allocation overhead |
| Hierarchical indices | BVH-based search | handle clustered and non-uniform distributions |
| Dynamic strategies | reuse, refit, partial update, rebuild | reduce per-step maintenance cost |
| Adaptive policies | online index and parameter selection | approach the fastest method for the current workload |
| Parallel variants | multicore CPU and GPU implementations | study scalability and hardware crossover points |

No method is assumed to be universally best. The goal is to identify the workload regions in which each approach is competitive and to compare an adaptive policy with fixed methods and an oracle baseline.

## Experimental workloads

The benchmark suite will include controlled particle distributions and motion models:

- uniform distributions;
- sparse domains;
- one or several dense clusters;
- moving clusters;
- rapidly changing distributions;
- different particle counts and search radii;
- later, variable-density and variable-radius scenarios.

Each optimized implementation will be checked against the brute-force reference.

## Evaluation metrics

### Correctness

- exact agreement with brute-force neighbor pairs;
- duplicate and missing pair detection;
- deterministic result validation where applicable.

### Performance

- index construction time;
- update, refit, reuse, and rebuild time;
- neighbor-search latency;
- particles and queries processed per second;
- candidate checks and accepted neighbor pairs;
- speedup over brute force and fixed-index baselines.

### Memory and scalability

- bytes per particle;
- index and neighbor-list memory;
- scaling with particle count;
- multicore efficiency;
- later, CPU/GPU crossover behavior.

### Adaptive quality

- method-selection accuracy;
- overhead of feature collection and decision making;
- regret relative to an oracle that knows the fastest method in advance;
- stability under changing workloads.

## Experimental methodology

Experiments will separate:

- workload generation;
- index construction or update;
- candidate traversal;
- exact distance checks;
- result materialization;
- correctness validation;
- CSV export and analysis.

Every report should record the compiler, optimization flags, CPU/GPU model, thread count, particle count, domain size, radius, distribution parameters, movement model, warm-up policy, repetitions, and summary statistics.

## Roadmap

- [ ] C++20 project infrastructure
- [ ] 2D particle and workload representation
- [ ] brute-force correctness baseline
- [ ] dense uniform-grid implementation
- [ ] reproducible workload generators and benchmarks
- [ ] clustered and dynamically changing scenarios
- [ ] hashed-grid implementation
- [ ] spatial sorting and contiguous storage
- [ ] index reuse and rebuild experiments
- [ ] workload feature collection
- [ ] online adaptive method selection
- [ ] BVH-based baseline
- [ ] multicore CPU implementations
- [ ] 3D workloads
- [ ] GPU implementations and CPU/GPU selection

## Planned repository structure

```text
adaptive-spatial-indexing/
├── include/                 # public C++ interfaces
├── src/                     # index implementations
├── tests/                   # correctness tests against brute force
├── benchmarks/              # microbenchmarks and scenario benchmarks
├── apps/                    # experiment runners and CLI tools
├── experiments/
│   ├── configs/             # reproducible workload definitions
│   ├── results/             # generated CSV data
│   └── scripts/             # Python analysis and plotting
└── reports/                 # tables, figures, and technical notes
```

## Current status

**Planned / research design stage.**

The first implementation phase will be CPU-only and deliberately narrow: 2D particles, brute force, a uniform grid, correctness tests, and reproducible benchmarks.

BVHs, adaptive policies, GPU acceleration, and advanced dynamic-update strategies will be added only after the baseline methodology is reliable.

## Technology direction

- C++20;
- CMake;
- GoogleTest;
- Google Benchmark;
- sanitizers;
- Python for result analysis and plotting;
- OpenMP later;
- CUDA later.

## License

This project is licensed under the MIT License.
