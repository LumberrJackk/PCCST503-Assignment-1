# PCCST503 – Machine Learning
## Assignment 1: Design of a Safe Semantic Planner in a Finite Cartesian State Space

This repository contains a complete C++ implementation, design report, experimental results, and user manual for Assignment 1.

### Chosen algorithm
**D* Lite** is used because the assignment explicitly permits D* Lite and requires replanning when transition availability, transitions, or the goal changes.

### Features implemented
- Finite Cartesian state representation using `uint64_t` IDs and `vector<double>` embeddings.
- Directed transitions with cost, safety, reliability, and availability.
- Initial and goal state handling.
- Bad-state avoidance: bad states are never expanded or selected for a path.
- Safety-aware optimization using Euclidean distance to the nearest bad state.
- Reliability-aware transition weighting.
- D* Lite incremental replanning for transition availability changes.
- Goal update with graph/safety data reused.
- Transition insertion and replanning.
- Metrics required by the assignment: goal success, bad states visited, path cost, minimum safety distance, explored states, planning time, memory usage, and replanning time.
- Six illustrative test cases from the assignment.

### Project structure
```text
PCCST503_Assignment1/
├── src/
│   └── main.cpp
├── docs/
│   ├── design_report.md
│   └── user_manual.md
├── results/
│   └── experimental_results.txt
├── tests/
│   └── test_cases.md
├── CMakeLists.txt
├── .gitignore
└── README.md
```

### Requirements
- C++17 compatible compiler
- CMake 3.15+ (optional; direct `g++` compilation is also supported)

### Compile and run with g++
```bash
g++ -std=c++17 -O2 -Wall -Wextra -pedantic src/main.cpp -o planner
./planner
```

### Compile with CMake
```bash
mkdir build
cd build
cmake ..
cmake --build .
./safe_planner
```

### Algorithm summary
The implementation uses D* Lite's `g`, `rhs`, priority queue, and predecessor/successor graph structures. The effective transition weight is:

`effective_cost = transition_cost + safety_penalty + reliability_penalty`

where the safety penalty increases when the destination state is close to a bad state, and the reliability penalty increases as transition reliability decreases. Bad states are hard constraints and are therefore excluded rather than merely penalized.

The heuristic is a scaled Euclidean distance. The scale is chosen from the minimum effective-cost-per-unit-distance among usable transitions, keeping the heuristic a lower bound for the effective edge cost under the implemented model.

### Important note about GitHub
The assignment package is complete locally. A GitHub repository cannot be created or pushed from this environment because there is no authenticated GitHub connection available. The final section of the user manual gives the exact commands to create the GitHub repository and push these files.
