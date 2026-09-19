High-performance computing (HPC) environments  (i.e. supercomputers) are very different to the average person's experience with computer systems. However, as someone who uses a Unix environment and it's command line for software development on the daily, I had assumed I would have been well accustomed to approaching a HPC environment beyond learning a few tools.

Around the 6th of August (2026) I set out to run the newly created ```test_implementations``` executable on the NCI's Gadi supercomputer. A positive test result would be significant for the project. Furthermore, the rare opportunity for hands on learning with a HPC environment, its tools, processes, and associated software is possibly the most direct path towards advancing my career in HPC (*Use of Tools and Technologies 1 and 3*). During the following week however, I would have my assumptions and technical confidence bluntly challenged.

Learning to use the Gadi supercomputing environment involved learning the following concepts, tools, and processes, specific to HPC:
- Separation of login, data-mover, and compute nodes (e.g. ```gadi.nci.org.au``` vs ```gadi-dm.nci.org.au```);
- Specialised directories (e,g, ```/home```, ```/scratch```, and ```/g/data```);
- Project resource allocations
   and quotas (e.g. ```lquota```, ```quota```, ```nci_account -P```);
- Module management (e.g. ```module avail/load/purge```);
- PBS job submission scripts (e.g. ```qsub```);
- And job monitoring (e.g. ```qstat` -swx```).

The above did not prove exceptionally difficult to learn. My learning and use of all of the above is clearly showcased in ```./Artifacts/Gadi_Build_Script.md``` where many of the tools can be seen explicitly written in the bash script while others are implicitly used (see the *Things to Note* section).

Significant difficulty came when naively attempting to directly apply my pre-established understanding of build systems (e.g. CMake and ```make```) to the Gadi system and would necessitate an adapting the methods with which I'm comfortable (*Initiative and Enterprise 1*). T8code, and by extension this project, relies on other software libraries called dependencies. The project's default configuration relied on ```VTK``` which significantly increased the number and complexity of the dependencies. For the extent of my software development experience dependency number and complexity has not been a problem and could be easily handled with Linux package managers (e.g. ```pacman``` or ```apt```). HPC environments are not typically equip with a package manager (such is the case with Gadi), therefore dependencies must be manually build or, preferably, integrated into a build script, both of which are non-trivial and increase the long-term fragility of the project (*Planning and Organisation 3*). Learning to reduce project dependencies, understand CMake's ```FetchContent``` and linker flags functionality in greater detail, and use more complex bash scripting became crucial to completing the build script.

# Should Rewrite