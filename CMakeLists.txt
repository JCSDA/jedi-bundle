# (C) Copyright 2022 UCAR
#

cmake_minimum_required( VERSION 3.12 FATAL_ERROR )

find_package( ecbuild 3.6 REQUIRED HINTS ${CMAKE_CURRENT_SOURCE_DIR} ${CMAKE_CURRENT_SOURCE_DIR}/../ecbuild)

project( jedi-bundle VERSION 1.0.0 LANGUAGES C CXX Fortran )

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
  ecbuild_bundle( PROJECT jedicmake GIT "https://github.com/jcsda-internal/jedi-cmake.git" TAG 1.3.0 )
  include( jedicmake/cmake/Functions/git_functions.cmake )
endif()

#ecbuild_bundle( PROJECT eckit    GIT "https://github.com/ecmwf/eckit.git" TAG 1.19.0 )
#ecbuild_bundle( PROJECT fckit    GIT "https://github.com/ecmwf/fckit.git" TAG 0.9.5 )
#ecbuild_bundle( PROJECT atlas    GIT "https://github.com/ecmwf/atlas.git" TAG 0.29.0 )

ecbuild_bundle( PROJECT oops     GIT "https://github.com/jcsda-internal/oops.git"        TAG 1.3.0 )
ecbuild_bundle( PROJECT vader    GIT "https://github.com/jcsda-internal/vader.git"       TAG 1.0.0 )
ecbuild_bundle( PROJECT saber    GIT "https://github.com/jcsda-internal/saber.git"       TAG 1.3.0 )

ecbuild_bundle( PROJECT crtm     GIT "https://github.com/jcsda-internal/crtm.git"        TAG v2.3-jedi.1 )
ecbuild_bundle( PROJECT gsw      GIT "https://github.com/jcsda-internal/GSW-Fortran.git" TAG v3.06 )
ecbuild_bundle( PROJECT ioda     GIT "https://github.com/jcsda-internal/ioda.git"        TAG 2.2.0 )
ecbuild_bundle( PROJECT ufo      GIT "https://github.com/jcsda-internal/ufo.git"         TAG 1.3.0 )

ecbuild_bundle( PROJECT fms         GIT "https://github.com/jcsda/FMS.git"                           TAG 1.2.0.jcsda )
ecbuild_bundle( PROJECT fv3         GIT "https://github.com/jcsda/GFDL_atmos_cubed_sphere.git"       TAG 1.2.0.jcsda )
ecbuild_bundle( PROJECT femps       GIT "https://github.com/jcsda-internal/femps.git"                TAG 1.2.0 )
ecbuild_bundle( PROJECT fv3-jedi-lm GIT "https://github.com/jcsda-internal/fv3-jedi-linearmodel.git" TAG 1.2.0 )
ecbuild_bundle( PROJECT fv3-jedi    GIT "https://github.com/jcsda-internal/fv3-jedi.git"             TAG 1.2.0 )

ecbuild_bundle( PROJECT mom6        GIT "https://github.com/jcsda-internal/MOM6.git"            TAG 2022.1.0 RECURSIVE )
ecbuild_bundle( PROJECT soca        GIT "https://github.com/jcsda-internal/soca.git"            TAG 1.1.0 )

#ecbuild_bundle( PROJECT saber-data     GIT "https://github.com/JCSDA-internal/saber-data.git"     TAG 1.3.0 )
#ecbuild_bundle( PROJECT ioda-data      GIT "https://github.com/JCSDA-internal/ioda-data.git"      TAG 2.2.0 )
#ecbuild_bundle( PROJECT ufo-data       GIT "https://github.com/JCSDA-internal/ufo-data.git"       TAG 1.3.0 )
#ecbuild_bundle( PROJECT fv3-jedi-data  GIT "https://github.com/JCSDA-internal/fv3-jedi-data.git"  TAG 1.2.0 )

ecbuild_bundle_finalize()
