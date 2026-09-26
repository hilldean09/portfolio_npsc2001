
---
Created : 2026-09-26
---

The formal title of my project, as proposed, is "Tree-based Adaptive Mesh Refinement in Gridap.jl." Gridap.jl is an open-source finite-element partial differential equation solver. Currently this likely stands as a mouthful of jargon, so for a quick term breakdown:
- Partial differential equations (PDEs) are a specific type of differential equations (equations that solve for a function by incorporating it's derivatives) and appear very frequently in engineering and physics as many different physical phenomena can be described using PDEs (e.g. heat flow, quantum wave packets, structural stress, fluid dynamics).
- The finite-element method (FEM) is a method for reducing the infinite complexity of relevant function spaces (sets of all possible functions fulfilling some conditions) to a finite complexity that computers can handle (specifically by approximating the solution with, typically, a piecewise polynomial function) by discretising the domain, i.e. making a computer mesh of the physical system.
- Tree-based adaptive mesh refinement (AMR) is a method for dynamically adapting the discretisation (mesh) by detecting areas of high-complexity (e.g. the centre of a whirlpool) and making said areas finer, i.e. refining the mesh, to make the solution more accurate without increasing the refinement level of the whole mesh which would take considerably more computational resources. 

As tree-based adaptive mesh refinement is a very complex algorithm, especially when targeting supercomputing environments, and there already exists an excellent library called T8code, the goal of the project is more so the integration of T8code into Gridap.jl. The integration of T8code into Gridap.jl is non-trivial for a few reasons:
1) Gridap.jl is written in Julia (the programming language), an interpreted language that is excellent for mathematical computing, even in HPC environments, while T8code is written in the compiled language C++. We thus have an instance of the Two-language Problem.
2) Gridap.jl and T8code have different mesh conformity requirements (relates to the computational representation of elements with respect to each other).

My contribution aims to resolve the aforementioned issues and create a high-level user interface.

# Some Concepts You Will See Throughout

## Topology Aware Global Vertex Indexing/Enumeration Algorithm

A core algorithm to resolve the mesh conformity issue is producing a global enumeration of the vertices of the discretisation, i.e. mesh, that is uniquely labelling every vertex with a $1, 2, 3 \dots$




