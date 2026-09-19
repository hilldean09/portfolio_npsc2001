---
Date : 2026-08-17
---
`
Around the 6th of August (2026) I set out to run the newly created ```test_implementations``` executable on the NCI's Gadi supercomputer. A positive test result would be significant for the project. Furthermore, the rare opportunity for hands on learning with a HPC environment, its tools, processes, and associated software is possibly the most direct path towards advancing my career in HPC. During the following week however, I would have my assumptions and technical confidence bluntly challenged.

I learnt much of the basics of using a HPC environment without significant difficulty (see *Appendix A*). Evidence of my learning can be clearly seen in *Artefact: ```Gadi_Build_Script.md```* (build scripts will be explained later). In the script many of the tools can be seen explicitly written (e.g. ```#PBDS ...``` and ```module ...```), while others are implicitly used (e.g. resource and filesystem structures). Learning these HPC specific tools directly advances *Use of Tools and Technology 1 & 3* and demonstrates my outlined conditions for evidencing improvement.

Where my preconceptions and technical confidence would actually show it's cracks was when approaching the problem of how to build the project library on Gadi. The project code relies on a number of third-party libraries (beyond T8code), these are called dependencies and must be compiled before the project's own libraries. For the extent of my software development experience dependencies have rarely been an issue through the use of Linux package managers (e.g. ```apt``` and ```pacman```). HPC environments however typically do not have package managers, instead many dependencies must be compiled from source on demand. The process of compiling these dependencies and the project's code itself can be automated via a bash build script. In it's default configuration the project depends on a library called VTK, which itself depends on a number of otherwise unneeded libraries. The complexity and long-term fragility of a build script scales non-trivially with the number of third-party dependencies it must handle (*Planning and Organisation 3*). Additionally, accurately and flexibly compiling dependencies for other dependencies can introduce issues due to obscure feature requirements. Finally, even linking against already libraries already available on Gadi can require the use of new CMake features.

Ultimately, the task I had naively assumed would take me a weekend took me over a week due to debugging the build script, reflecting a notable failure in my time-management skills as a result of false confidence (*Planning and Organisation 1*). To complete the build script I had to:
1) Reduce dependencies via CMake build flags (compare *Artefact: ```Dependency_Graph.svg```* and *Artefact: ```Refined_Dependency_Graph.svg```*);
2) Manipulate CMake's ```FetchContent``` function to improve the build script's long-term robustness;
3) And chain bash scripting features in more complex ways to improve the script's portability.

The design considerations and additional technical investments in the script for benefit of future works fulfil my outlined requirements for evidencing improvement in *Planning and Organisation 3*.

Failing so notably for an extended time in an area I had grown arguably too comfortable in has been both an uncomfortable and beneficial experience. The experience has advanced my understanding of software development in HPC environments and swiftly readjusted my preconceptions and expectations. In the future I will note to be more wary of learning new computing environments and better interrogate the eases I take for granted regarding software development.


# Appendix

## A) Gadi Concepts, Tools, and Processes
Learning to use the Gadi supercomputing environment involved learning the following concepts, tools, and processes, specific to HPC:
- Separation of login, data-mover, and compute nodes (e.g. ```gadi.nci.org.au``` vs ```gadi-dm.nci.org.au```);
- Specialised directories (e,g, ```/home```, ```/scratch```, and ```/g/data```);
- Project resource allocations
   and quotas (e.g. ```lquota```, ```quota```, and ```nci_account -P```);
- Module management (e.g. ```module avail/load/purge```);
- PBS job submission scripts (e.g. ```#PBS ...``` and```qsub```);
- And job monitoring (e.g. ```qstat` -swx```).

