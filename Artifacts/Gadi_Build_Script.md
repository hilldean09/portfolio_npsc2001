The following is the PBS job submission / library build script (creating ```test_implementations```), copied on the 17th of August (2026). 

## Things to Note:
- The "PBS header" (lines preceded by ```#PBS```) to request compute resources.
- The modules section (section headered by ```##### Modules #####```).
- The ```t8code``` section (section headered by ```##### T8code #####```).

```bash
#!/bin/bash

#PBS -l ncpus=8
#PBS -l mem=32GB
#PBS -l jobfs=5GB
#PBS -q normal
#PBS -P kr97
#PBS -l walltime=00:30:00
#PBS -l storage=scratch/kr97
#PBS -l wd

# Script to build on Gadi
# - Disables T8code VTK to significantly
#   reduce dependency chain.

# Better error diagnostics
set -euo pipefail

# Steps :
# (1) Import modules
# (2) Build Zlib
# (3) Build libsc
# (4) Build p4est
# (5) Build T8code
# (6) Build T82G

##### Modules ######

module purge

module load gcc/15.1.0
module load openmpi/5.0.8
module load cmake/4.3.3

module list


##### Setup #####

export EXECUTABLE_NAME=test_implementations
export PROJECT_ID=kr97
export SOURCE_DIRECTORY=$HOME/repos
export INSTALL_PREFIX=/scratch/${PROJECT_ID}/${USER}/builds
export MPI_INCLUDE_PATH=/apps/openmpi/5.0.8/include

mkdir -p "$INSTALL_PREFIX"

export CMAKE_PREFIX_PATH="$INSTALL_PREFIX:${CMAKE_PREFIX_PATH:-}"

# Uses PBS for number of cpus, else
# defaults to using the nprocs command
NPROCS=${PBS_NCPUS:-${nprocs}}


##### ZLIB #####

mkdir -p "${SOURCE_DIRECTORY}/zlib/build"
cd "${SOURCE_DIRECTORY}/zlib/build"

cmake -S .. -B . \
  -DCMAKE_BUILD_TYPE=Release \
  -DCMAKE_INSTALL_PREFIX="$INSTALL_PREFIX" \
  -DCMAKE_PREFIX_PATH="$INSTALL_PREFIX" \
  -DMPI_C_COMPILER=$(which mpicc) \
  -DMPI_C_HEADER_DIR="$MPI_INCLUDE_PATH"


make -j"$NPROCS"
make install

##### T8code #####

mkdir -p "${SOURCE_DIRECTORY}/t8code/build"
cd "${SOURCE_DIRECTORY}/t8code/build"

cmake -S .. -B . \
  -DCMAKE_BUILD_TYPE=RelWithDebInfo \
  -DCMAKE_INSTALL_PREFIX="$INSTALL_PREFIX" \
  -DCMAKE_PREFIX_PATH="$INSTALL_PREFIX" \
  -DT8CODE_ENABLE_VTK=OFF \
  -DT8CODE_BUILD_TESTS=OFF \
  -DT8CODE_BUILD_TUTORIALS=OFF \
  -DT8CODE_BUILD_BENCHMARKS=OFF \
  -DMPI_C_COMPILER=$(which mpicc) \
  -DMPI_CXX_COMPILER=$(which mpicxx) \
  -DMPI_C_HEADER_DIR="$MPI_INCLUDE_PATH" \
  -DMPI_CXX_HEADER_DIR="$MPI_INCLUDE_PATH" \
  -DFETCHCONTENT_SOURCE_DIR_GOOGLETEST="${SOURCE_DIRECTORY}/googletest" \
  -DFETCHCONTENT_SOURCE_DIR_SC="${SOURCE_DIRECTORY}/libsc" \
  -DFETCHCONTENT_SOURCE_DIR_P4EST="${SOURCE_DIRECTORY}/p4est"

make -j"$NPROCS"
make install


##### T82G #####

mkdir -p "${SOURCE_DIRECTORY}/t8code_to_gridap_notes_npsc2001/build"
cd "${SOURCE_DIRECTORY}/t8code_to_gridap_notes_npsc2001/build"

cmake -S .. -B . \
  -DCMAKE_BUILD_TYPE=RelWithDebInfo \
  -DCMAKE_PREFIX_PATH="$INSTALL_PREFIX" \
  -DMPI_C_COMPILER=$(which mpicc) \
  -DMPI_C_HEADER_DIR="$MPI_INCLUDE_PATH" \
  -DMPI_CXX_COMPILER=$(which mpicxx) \
  -DMPI_CXX_HEADER_DIR="$MPI_INCLUDE_PATH"

make "$EXECUTABLE_NAME"
```