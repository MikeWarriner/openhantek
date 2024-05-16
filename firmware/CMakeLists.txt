project(FirmwareExtractor C)
cmake_minimum_required(VERSION 3.29)

CC_GCC_LTO_ZSTD=1
find_library( BFD_LIBRARY	NAMES libbfd.a PATHS /usr/lib /usr/lib64 /opt/homebrew/Cellar/binutils/2.42/lib)
find_path(BFD_INCLUDE bfd.h PATHS /usr/include
    /usr/local/include
    /opt/local/include
    /opt/homebrew/Cellar/binutils/2.42/include
    /sw/include)


if (NOT BFD_INCLUDE)
    message(STATUS "BFD INCLUDE not found. Please install binutils-devel (fedora) / binutils-dev (ubuntu)")
    return()
endif()

if (NOT BFD_LIBRARY)
    message(STATUS "BFD LIBRARY not found. Please install binutils-devel (fedora) / binutils-dev (ubuntu)")
    return()
endif()

add_executable(${PROJECT_NAME} extractfw.c)
target_link_libraries(${PROJECT_NAME} ${BFD_LIBRARY} )
target_include_directories(${PROJECT_NAME} PRIVATE ${BFD_INCLUDE})
