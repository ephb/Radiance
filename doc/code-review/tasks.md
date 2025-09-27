# Radiance C++17 Migration Tasks

This document provides a checklist of tasks for the Radiance C++17 migration project, based on the recommendations in the [code review report](report.md).

---

### Phase 1: Build System Consolidation
- [ ] **Enhance CMake Build:** Expand the existing `CMakeLists.txt` files to fully support all features and targets currently handled by the `makeall` and SCons build systems.
- [ ] **Integrate Testing:** Port the existing test suite (`makeall test`) to CTest, CMake's testing framework.
- [ ] **Deprecate Legacy Systems:** Once the CMake build is fully functional and validated, remove the `makeall` script, `Rmakefile` files, and `SConstruct` files.

### Phase 2: Incremental C-to-C++ Conversion
- [ ] **Configure for C++17:** Set the compiler to C++17 and begin converting `.c` files to `.cpp`.
- [ ] **Initial Refactoring:** Address initial compiler errors (e.g., C-style casts).
- [ ] **Adopt C++ Idioms:**
    - [ ] Replace `malloc`/`free` with smart pointers (`std::unique_ptr`, `std::shared_ptr`).
    - [ ] Convert C-style structs to C++ classes.
    - [ ] Use standard library containers and algorithms.

### Phase 3: Modernize Threading
- [ ] **Refactor `rtrace` Parallelism:**
    - [ ] Replace the `fork()`-based parallelism in `rtrace` with a C++ thread pool.
    - [ ] Implement a thread-safe task queue for rays.
- [ ] **Refactor General Threading:**
    - [ ] Replace custom threading wrappers (e.g., in `src/gen/atmos.c`) with `std::thread`, `std::mutex`, etc.

### Phase 4: Performance Optimization
- [ ] **Profile the Application:** Identify performance bottlenecks in the modernized codebase.
- [ ] **Apply Parallel Algorithms:** Use C++17's parallel algorithms to optimize data-parallel operations.
- [ ] **Investigate SIMD:** Explore using SIMD intrinsics for core ray-tracing calculations.
- [ ] **Iterate and Test:** Continuously measure performance and run regression tests to ensure scientific accuracy.