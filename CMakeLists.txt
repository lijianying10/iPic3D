cmake_minimum_required(VERSION 2.8.8)

#
# Project declaration
#

project(iPic3D)

#
# Set compiler
#

SET(CMAKE_C_COMPILER /opt/intel/impi/4.1.1.036/bin64/mpicc)
SET(CMAKE_CXX_COMPILER /opt/intel/impi/4.1.1.036/bin64/mpicxx)

#
# Set exec path
#

set(EXECUTABLE_OUTPUT_PATH work/${CMAKE_BUILD_TYPE})
set(LIBRARY_OUTPUT_PATH lib)

#
# Find third class libraries
#

#find_package(HDF5 COMPONENTS HL C REQUIRED)
#find_package(MPI REQUIRED)
set(HDF5_INCLUDE_DIRS /opt/hdf5/include/)
set(MPI_INCLUDE_PATH  /opt/intel/impi/4.1.1.036/intel64/include/)
set(FFTW_INCLUDE_PATH  /opt/fftw/include)
set(HDF5_LIBRARY_DIRS /opt/hdf5/lib/)
set(MPI_LIBRARY_DIRS /opt/intel/impi/4.1.1.036/intel64/lib/)
set(FFTW_LIBRARY_DIRS /opt/fftw/lib)

#
# include and lib directories
#

include_directories(
        include
        ${HDF5_INCLUDE_DIRS}
        ${MPI_INCLUDE_PATH}
		  ${FFTW_INCLUDE_PATH}
)

link_directories(
        ${HDF5_LIBRARY_DIRS}
        ${MPI_LIBRARY_DIRS}
		 ${FFTW_LIBRARY_DIRS}
)

#
# Header file list
#

file(
        GLOB
        inc_files
        ConfigFile/src/*.h
        PSKOutput3D/*.h
        bc/*.h
        communication/*.h
        fields/*.h
        grids/*.h
        iPIC3D.h/*.h
        inputoutput/*.h
        mathlib/*.h
        mpidata/*.h
        particles/*.h
        performances/*.h
        processtopology/*.h
        solvers/*.h
        utility/*.h
)

#
# Source file list
#

file(
        GLOB
        src_files
        ConfigFile/src/*.cpp
        PSKOutput3D/*.cpp
        bc/*.cpp
        communication/*.cpp
        fields/*.cpp
        grids/*.cpp
        iPIC3D.cpp/*.cpp
        inputoutput/*.cpp
        mathlib/*.cpp
        mpidata/*.cpp
        particles/*.cpp
        performances/*.cpp
        processtopology/*.cpp
        solvers/*.cpp
        utility/*.cpp
        iPIC3D.cpp
)

#
# Executable declaration
#

add_executable(
        iPIC3D
        ${inc_files}
        ${src_files}
)

#
# Link external libraries
#

target_link_libraries(
			iPIC3D
			hdf5_cpp
			hdf5_hl_cpp
			hdf5
			hdf5_hl
)

