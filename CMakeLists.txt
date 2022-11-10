# Note - as of Nov 7, 2022, the main branch of this repository is frozen. The develop branch is used for all releases and all developments.

# (C) Copyright 2022 UCAR
#

cmake_minimum_required( VERSION 3.12 FATAL_ERROR )

find_package( ecbuild 3.6 REQUIRED HINTS ${CMAKE_CURRENT_SOURCE_DIR} ${CMAKE_CURRENT_SOURCE_DIR}/../ecbuild)

project( jedi-bundle VERSION 2.0.0 LANGUAGES C CXX Fortran )

list(APPEND CMAKE_MODULE_PATH "${CMAKE_CURRENT_SOURCE_DIR}/cmake")

include( ecbuild_bundle )

# Default release mode
set( ECBUILD_DEFAULT_BUILD_TYPE Release )

# Enable OpenMP and MPI
set( ENABLE_MPI ON CACHE BOOL "Compile with MPI" )
set( ENABLE_OMP ON CACHE BOOL "Compile with OpenMP" )

# Define bundle
ecbuild_bundle_initialize()

# Use external jedi-cmake or build in bundle
if(DEFINED ENV{jedi_cmake_ROOT})
  include( $ENV{jedi_cmake_ROOT}/share/jedicmake/Functions/git_functions.cmake )
else()
  ecbuild_bundle( PROJECT jedicmake GIT "https://github.com/jcsda/jedi-cmake.git" TAG 1.4.0 RECURSIVE )
  include( jedicmake/cmake/Functions/git_functions.cmake )
endif()

#ecbuild_bundle( PROJECT eckit    GIT "https://github.com/ecmwf/eckit.git" TAG 1.19.0 )
#ecbuild_bundle( PROJECT fckit    GIT "https://github.com/ecmwf/fckit.git" TAG 0.9.5 )
#ecbuild_bundle( PROJECT atlas    GIT "https://github.com/ecmwf/atlas.git" TAG 0.30.0 )

ecbuild_bundle( PROJECT oops     GIT "https://github.com/jcsda/oops.git"        TAG 1.4.0 )
ecbuild_bundle( PROJECT vader    GIT "https://github.com/jcsda/vader.git"       TAG 1.1.0 )
ecbuild_bundle( PROJECT saber    GIT "https://github.com/jcsda/saber.git"       TAG 1.4.0 )

#ecbuild_bundle( PROJECT crtm     GIT "https://github.com/jcsda/crtm.git"        TAG v2.4-jedi )
ecbuild_bundle( PROJECT gsw      GIT "https://github.com/jcsda/GSW-Fortran.git" TAG v3.07 )
ecbuild_bundle( PROJECT ioda     GIT "https://github.com/jcsda/ioda.git"        TAG 2.3.0 )
ecbuild_bundle( PROJECT ufo      GIT "https://github.com/jcsda/ufo.git"         TAG 1.4.0 )

#ecbuild_bundle( PROJECT fms         GIT "https://github.com/jcsda/FMS.git"                           TAG 1.2.0.jcsda )
ecbuild_bundle( PROJECT fv3         GIT "https://github.com/jcsda/GFDL_atmos_cubed_sphere.git"       TAG 1.2.0.jcsda )
ecbuild_bundle( PROJECT femps       GIT "https://github.com/jcsda/femps.git"                         TAG 1.2.0 )
ecbuild_bundle( PROJECT fv3-jedi-lm GIT "https://github.com/jcsda/fv3-jedi-linearmodel.git"          TAG 1.2.0 )
ecbuild_bundle( PROJECT fv3-jedi    GIT "https://github.com/jcsda/fv3-jedi.git"                      TAG 1.3.0 )

ecbuild_bundle( PROJECT mom6        GIT "https://github.com/jcsda/MOM6.git"            TAG 2022.1.0 RECURSIVE )
ecbuild_bundle( PROJECT soca        GIT "https://github.com/jcsda/soca.git"            TAG 1.2.0 )

ecbuild_bundle_finalize()

