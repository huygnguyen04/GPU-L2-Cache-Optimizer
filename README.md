# GPU-L2-Cache-Optimizer

## 📑 Documentation
### 📄 [**Final Report**](./HuyNguyen_L2Cache_FinalReport.pdf) - Full analysis of cache scaling experiments, architectural insights, and hardware modeling.
### 📄 [**Research Proposal**](./HuyNguyen_Research_Proposal.pdf) - Initial background, motivation, and project plan.
### 🎞️ [**Presentation Slides**](https://docs.google.com/presentation/d/1fhQBrdnbD1-Ip40FcdpEZ-8poqQesz_WVgXzYtwDN4A/edit?usp=sharing) - Slide deck covering methodology and key results.

---

This project explores the simulation and optimization of extended L2 cache architectures in GPUs using **GPGPU-Sim**, with the goal of improving performance for memory-bound CUDA workloads. It combines architectural experimentation, benchmark profiling, and area-energy tradeoff analysis to guide future GPU memory hierarchy design.

**Author**: Huy G Nguyen  
**Advisor**: Prof. Kevin Skadron  
**Department of Computer Science, University of Virginia**

## 🔍 Project Overview

Modern GPU workloads in high-performance computing (HPC) and machine learning frequently encounter memory bottlenecks due to limited on-chip L2 cache capacity. This project investigates the performance and efficiency impact of extending L2 cache size by adjusting associativity and set count.

Benchmarks from the Rodinia suite—including **BFS**, **K-Means**, **Gaussian Elimination**, **Needleman-Wunsch**, **LU Decomposition**, and **DWT2D**—are analyzed using **GPGPU-Sim**, with cache energy/area modeled using **CACTI 6.5**.

## 🚀 Key Contributions

- **Performance Gains**: Larger L2 caches significantly reduce memory stalls and DRAM traffic for memory-bound workloads.
- **Workload Sensitivity**: Applications with high L2 miss rates and strong spatial/temporal locality (e.g., NW, DWT2D) see the most benefit.
- **Design Tradeoffs**:
  - Associativity scaling reduces conflict misses in irregular patterns.
  - Set count scaling helps with large working sets.
  - Gains plateau beyond 2–4× L2 size increases.
- **Hardware Cost**: Larger caches increase area and dynamic energy by 2–2.5×, necessitating workload-aware cache sizing.

## 🧪 Tools & Benchmarks

- **Simulator**: GPGPU-Sim v4.0 (Volta V100 config)
- **Modeling Tool**: CACTI 6.5 (32nm, 128B line)
- **Benchmarks**:
  - Memory-bound: BFS, KMeans, Gaussian, NW, LUD, DWT2D
  - Compute-bound (control): Nearest Neighbor, Pathfinder

## 📈 Results Summary

Extending L2 cache size yielded up to **50% performance improvement** for memory-bound CUDA applications with large working sets. In contrast, compute-bound benchmarks showed negligible gains, reinforcing that cache scaling is workload-sensitive.

- **Associativity scaling**: Best for reducing conflict misses in irregular workloads (e.g., Gaussian, LUD).
- **Set count scaling**: Best for large spatially-reused datasets (e.g., KMeans, DWT2D).
- **Tradeoff**: Quadrupling L2 size significantly increases area/energy (~2.5×), so optimization must consider system constraints.

## 🔮 Future Work

- Extend analysis to **PPA (performance-per-area)** and **ED² (energy-delay²)** metrics
- Analyze **deeper input size ranges** to identify L2 stress thresholds
- Evaluate **new GPU architectures** (varying SM/core count, L1 size)
- Explore **software-level optimizations** (prefetching, data placement)
- Test on **ML workloads** like CNNs and Transformers
- Use **Roofline modeling** for further compute-bound analysis

## 📝 License

This project is licensed under the [MIT License](LICENSE) - see the LICENSE file for details.

---

*This work provides foundational insight into L2 cache scaling for future GPU architectures, especially in the context of AI and HPC workloads.*
