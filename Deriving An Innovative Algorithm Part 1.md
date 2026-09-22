
---
Created : 2026-09-21
---

This reflection, due to the significance of the underlying event is part 1 of 2, and includes some more technical concepts, however these are not core to the purpose of the reflection.

# The Background

When the project pivoted from using geometric properties (e.g. coordinates) to derive a global vertex indexing (a way of ordering all the vertices of a mesh) to using topological properties (how mesh element, e.g. triangles, tetrahedra, connect) the first priority was developing/researching a suitable algorithm. In the process I constructed an algorithm, acknowledged verbally by Dr. Alberto Martin as being unique (and later given feedback on by Prof. Victor Calo with the use of Claude).

The process of identifying developing an algorithm, comparing it to alternatives, and clarifying priorities was incredibly insightful into how real HPC researchers work. My notes on the process, in which I focused on formalising my logic and arguments, can be found in *Artefact: ```Weekly-Log-2026-05-05.md```* (note that this artefact contains multiple different sections which would be considered artefacts on their own).

*Artefact: ```Weekly-Log-2026-05-05.md```* evidences improvement in a number of categories I identified in my Independent Study Contract (ISC), primarily *Problem Identification and Solution 2 & 3*, *Teamwork 1 & 2*, *Communication 1 & 3*, and *Initiative and Enterprise 3*. I will only address *Problem Identification and Solution 2 & 3* and *Initiative and Enterprise 3* here (part 1) for brevity.

# The Reflection

To develop a topology-aware global vertex indexing algorithm I began with an intuitive mental model of walking a path around a vertex from an initial element, identifying which elements touch said vertex. By enforcing a strict order in which elements and corners are visited we can easily identify vertices that have already been scanned and stored, thus producing a global vertex indexing. Formalising the mental model was, naturally, significantly more difficult. The formal psuedo-code can be found in *Artefact: ```Weekly-Log-2026-05-05.md```* labelled as the alternative algorithm corner-depth-first-search (CDFS).

The algorithm, while found to be significantly worse for our purpose, had advantages over the more-recognised alternative we ultimately used, vertex-equivalence disjoint-set-unions (VDSU), in different use cases. An example of where the algorithm I developed is preferable is spontaneous vertex-equivalence checks (as opposed to frequent mesh-wide checks), as it is only concerned with local structure about a single vertex and does not require decoding face-orientation. Additionally, my algorithm can be easily applied to arbitrary dimensional meshes. Dr. Alberto Martin acknowledged the corner-local graph-based equivalence algorithm as being unique and not something he had come across.

A specific achievement outcome I identified in my Independent Study Contract (ISC) (*Innovation and Enterprise 3*), and that became a strong personal goal of mine, was creating a small truly innovative algorithm/method. I believe that the CDFS algorithm fulfills my goal as a small concrete innovation, although not for our application. I believe the analysis of my CDFS algorithm against an unused alternative, dubbed GBFS, (seen in *Artefact: ```Weekly-Log-2026-05-05.md```*) highlights my deepening understanding of high-performance computing and growing ability to make innovative design decisions within the field.

I believe that the area I grew the most in was formalising my ideas, i.e. the CDFS algorithm, and my arguments for and against it's use. Formalising sequential ideas and arguments was an area I also identified in my ISC as a achievement outcome in *Problem Identification and Solution 2 & 3*, which I aimed to evidence with a record of formally synthesising an idea, as fulfilled by *Artefact: ```Weekly-Log-2026-05-05.md```*.

Rigorous and dependable algorithms in high-performance computing and mathematics hinges on sequential and formal construction, as well as structured analysis. Naturally experiencing the process of pondering and formalising an innovative algorithmic idea has significantly expanded my view on how real-research in the field is done, e.g. pseudo-code write ups, structured analysis of every relevant metric (good or bad for your algorithm), research priorities beyond performance and complexity (e.g. implementation time, longevity). The aforementioned experience, pretty self-evidently, has immediate benefit to my future in HPC and mathematics. 





