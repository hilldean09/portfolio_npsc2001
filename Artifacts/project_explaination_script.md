
This document records my "script" (in the sense of a patterned set of ideas) for explaining my project which I have developed over the year.

# The Explanation

My project is formally titled "Tree-based Adaptive Mesh Refinement in Gridap.jl", where Gridap.jl is a finite-element partial differential equation solver.

<ASK IF AUDIENCE IS FAMILIAR WITH PARTIAL DIFFERENTIAL EQUATIONS, IF NOT:> Partial differential equations are a specific type of equation that appear everywhere in physics and engineering, Schroedinger's equation, heat flow, stress, fluid mechanics, etc. Solving them allows us to simulate lots of different systems.

The finite-element method is a way of reducing the infinite complexity of all possible functions to the finite complexity of simple piecewise functions across a discretisation of the domain, i.e. what we are simulating. Think of a capture reducing the infinite complexity of the real world into a grid of pixels. The finite complexity allows computers to approximate solutions to these partial differential equations. The finer or more refined the discretisation of the domain, i.e. the resolution, the more accurate the approximation is but the more computationally demanding the problem becomes.

Now lets consider simulating a whirlpool in a large body of water. The water far away from the whirlpool is quite calm, its movement isn't very complex, therefore we don't need much refinement to achieve high simulation accuracy; think about taking a high resolution picture versus a low resolution picture that is entirely blue. However the water at the center of the whirlpool is very complex, there's twisting, plashing, etc, therefore we want to simulate this area with a finer refinement to accurately capture the behaviour of the water; again, think taking a high resolution versus a low resolution picture of a scene with lots of tiny details. We would like to be algorithmically determine which areas are more complex than others so we can adaptively refine, i.e. increase the resolution, of these areas. This is the purpose of tree-based adaptive mesh refinement, which achieves this goal using tree-based data structures.

Tree-based adaptive mesh refinement is very hard to do well, especially for high-performance computing, thankfully there exists a well-established open-source library out of Germany called T8code which does tree-based adaptive mesh refinement. The problem lies in that T8code and Gridap.jl impose different requirements on the topological. <DO H1 CONFORMITY FINGER DEMONSTRATION>. Fixing this is my task as well bridging T8code, written in C++, and Gridap.jl, written in Julia.


