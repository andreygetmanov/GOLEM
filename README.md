# GOLEM

---

![License](https://img.shields.io/github/license/andreygetmanov/GOLEM?style=flat&logo=opensourceinitiative&logoColor=white&color=blue)
[![OSA-improved](https://img.shields.io/badge/improved%20by-OSA-yellow)](https://github.com/aimclub/OSA)

Built with:

![numpy](https://img.shields.io/badge/NumPy-013243.svg?style={0}&logo=NumPy&logoColor=white)
![pandas](https://img.shields.io/badge/pandas-150458.svg?style={0}&logo=pandas&logoColor=white)
![pytest](https://img.shields.io/badge/Pytest-0A9EDC.svg?style={0}&logo=Pytest&logoColor=white)
![scipy](https://img.shields.io/badge/SciPy-8CAAE6.svg?style={0}&logo=SciPy&logoColor=white)
![tqdm](https://img.shields.io/badge/tqdm-FFC107.svg?style={0}&logo=tqdm&logoColor=black)

---

## Overview

GOLEM is an AI framework for tackling complex optimization problems using graph-based models and evolutionary algorithms. It helps users discover structured, interpretable solutions where traditional methods fall short, offering a versatile approach applicable to diverse fields like machine learning and scientific discovery.

---

## Table of Contents

- [Core features](#core-features)
- [Installation](#installation)
- [Getting Started](#getting-started)
- [Examples](#examples)
- [Documentation](#documentation)
- [Contributing](#contributing)
- [License](#license)
- [Citation](#citation)

---
## Core features

1. **Graph-Based Model Optimization**: GOLEM focuses on optimizing structured graph-based models, enabling solutions for complex problems where traditional gradient-based methods struggle.
2. **Metaheuristic Algorithms**: Utilizes metaheuristic methods (primarily evolutionary algorithms) to navigate complex problem spaces and find optimal or near-optimal solutions.
3. **Extensibility & Domain Adaptability**: Designed to be easily extended to new problem domains and customized with different graph structures and objective functions.
4. **Application Framework**: Serves as a foundational framework applicable to diverse areas like AutoML, Bayesian network structure search, differential equation discovery, and geometric design.

---

## Installation

Install GOLEM using one of the following methods:

**Build from source:**

1. Clone the GOLEM repository:
```sh
git clone https://github.com/andreygetmanov/GOLEM
```

2. Navigate to the project directory:
```sh
cd GOLEM
```

3. Install the project dependencies:

```sh
pip install -r requirements.txt
```

---

## Getting Started

To get started, you can install GOLEM using pip:

```bash
pip install thegolem
```

The `examples/synthetic_graph_evolution` directory provides several examples of how to use GOLEM for graph search. For instance, `simple_run.py`, `graph_search.py`, and `tree_search.py` demonstrate basic usage.

Here's a quick example from `simple_run.py`:

```python
def run_graph_search(size=16, timeout=8):
    # Generate target graph sought by optimizer using edit distance objective
    node_types = ('a', 'b')  # Available node types that can appear in graphs
    target_graph = generate_labeled_graph('tree', size, node_types)
    objective = Objective(partial(tree_edit_dist, target_graph))
    initial_population = [generate_labeled_graph('tree', 5, node_types) for _ in range(10)]

    # Setup optimization parameters
    requirements = GraphRequirements(timeout=timedelta(minutes=timeout))
    gen_params = GraphGenerationParams(adapter=BaseNetworkxAdapter(), available_node_types=node_types)
    algo_params = GPAlgorithmParameters(pop_size=30)

    # Build and run the optimizer
    optimiser = EvoGraphOptimizer(objective, initial_population, requirements, gen_params, algo_params)
    found_graphs = optimiser.optimise(objective)

    # Visualize results
    found_graph = gen_params.adapter.restore(found_graphs[0])  # Transform back to NetworkX graph
    draw_graphs_subplots(target_graph, found_graph, titles=['Target Graph', 'Found Graph'])
    optimiser.history.show.fitness_line()
    return found_graph
```

---

## Examples

Examples of how this should work and how it should be used are available [here](https://github.com/andreygetmanov/GOLEM/tree/main/docs/source/examples).

---

## Documentation

A detailed GOLEM description is available [here](https://thegolem.readthedocs.io).

---

## Contributing

- **[Report Issues](https://github.com/andreygetmanov/GOLEM/issues)**: Submit bugs found or log feature requests for the project.

---

## License

This project is protected under the BSD 3-Clause "New" or "Revised" License. For more details, refer to the [LICENSE](https://github.com/andreygetmanov/GOLEM/tree/main/LICENSE) file.

---

## Citation

If you use this software, please cite it as below.

### APA format:

    andreygetmanov (2025). GOLEM repository [Computer software]. https://github.com/andreygetmanov/GOLEM

### BibTeX format:

    @misc{GOLEM,

        author = {andreygetmanov},

        title = {GOLEM repository},

        year = {2025},

        publisher = {github.com},

        journal = {github.com repository},

        howpublished = {\url{https://github.com/andreygetmanov/GOLEM.git}},

        url = {https://github.com/andreygetmanov/GOLEM.git}

    }

---
