# This is the root ITK CMakeLists file.
cmake_minimum_required(VERSION 3.10.2)
if(COMMAND CMAKE_POLICY)
  CMAKE_POLICY(SET CMP0003 NEW)
endif(COMMAND CMAKE_POLICY)

# This project is designed to be built outside the Insight source tree.
project( PhaseSymmetryImageFilter)

# Find ITK.
find_package(ITK REQUIRED
  MODULE
  COMPONENTS PhaseSymmetry
    ITKIOMeta
    ITKIOTIFF
    ITKIOPNG
  )
include(${ITK_USE_FILE})

find_package( SlicerExecutionModel REQUIRED )
include( ${SlicerExecutionModel_USE_FILE} )

SEMMacroBuildCLI(
  NAME PhaseSymmetryFilter
  TARGET_LIBRARIES ${ITK_LIBRARIES}
  )

add_executable( PhaseSymmetryImageFilter2D main2.cxx)
target_link_libraries( PhaseSymmetryImageFilter2D ${ITK_LIBRARIES} )

add_executable( PhaseSymmetryImageFilter3D main3.cxx)
target_link_libraries( PhaseSymmetryImageFilter3D ${ITK_LIBRARIES} )
