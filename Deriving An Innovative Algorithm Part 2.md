
---
Created : 2026-09-21
---

This reflection, due to the significance of the underlying event is part 1 of 2, and includes some more technical concepts, however these are not core to the purpose of the reflection.

# The Background

When the project pivoted from using geometric properties (e.g. coordinates) to derive a global vertex indexing (a way of ordering all the vertices of a mesh) to using topological properties (how mesh element, e.g. triangles, tetrahedra, connect) the first priority was developing/researching a suitable algorithm. In the process I constructed an algorithm, acknowledged verbally by Dr. Alberto Martin as being unique (and later given feedback on by Prof. Victor Calo with the use of Claude).

The process of identifying developing an algorithm, comparing it to alternatives, and clarifying priorities was incredibly insightful into how real HPC researchers work. My notes on the process, in which I focused on formalising my logic and arguments, can be found in *Artefact: ```Weekly-Log-2026-05-05.md```* (note that this artefact contains multiple different sections which would be considered artefacts on their own).

*Artefact: ```Weekly-Log-2026-05-05.md```* evidences improvement in a number of categories I identified in my Independent Study Contract (ISC), primarily *Problem Identification and Solution 2 & 3*, *Teamwork 1 & 2*, *Communication 1 & 3*, and *Initiative and Enterprise 3*. Here (part 2), I will focus on *Teamwork 1 & 2* and *Communication 1 & 3* for brevity.

# The Reflection

This reflection relates to my notes on communication between my supervisors and myself regarding the development of a topology-aware global vertex indexing algorithm seen in *Artefact: ```Weekly-Log-2026-05-05.md```*.

When writing my Independent Study Contract (ISC), I did not expect to have the opportunity to achieve outcomes relating to collaborative work, being the only person working on my project, however, when discussing topology-aware global vertex indexing algorithms I had the opportunity to (non-trivially) exchange ideas with my supervisors. 

As the global vertex indexing algorithm is core to my project (allows use to establish H1-mesh conformity, a convenient mathematical property needed by Gridap.jl), ensuring it is accurate is of key importance. As T8code imposes a variety of limitations on the topological informations and methods available, there was no clear algorithm to reach for, thus my supervisors and I were thorough in discussing possible algorithms, and ultimately our goals (*Teamwork 1*). 

During the discussion, my first priority was expressing my ideas in a fluid and concise manner as to reduce the mental load of the already demanding technical concept and to respect my supervisors' time (*Communication 1*). Additionally, constructively critiquing my supervisors' suggestions, while uncomfortable given their expertise, was necessary (and eventually fruitful) and having said critiques validated and invalidated made me more comfortable broaching feedback (though still cautiously) to supervisors and those more technically capable/knowledgeable than me (*Teamwork 2*).



