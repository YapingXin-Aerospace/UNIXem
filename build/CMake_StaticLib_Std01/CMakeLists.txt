CMAKE_MINIMUM_REQUIRED (VERSION 3.14)
PROJECT (UNIXem C)

# Using C99
# Reference: https://stackoverflow.com/questions/24840030/forcing-c99-in-cmake-to-use-for-loop-initial-declaration
SET (CMAKE_C_STANDARD 99)

MESSAGE (STATUS "Solution: " ${CMAKE_PROJECT_NAME})
MESSAGE (STATUS "Dev-Root BINARY dir " ${PROJECT_BINARY_DIR})
MESSAGE (STATUS "Dev-Root SOURCE dir " ${PROJECT_SOURCE_DIR})

SET (REPO_Dev_DIR ${PROJECT_SOURCE_DIR}/../../)
MESSAGE (STATUS "REPO_Dev_DIR: " ${REPO_Dev_DIR})

# Check Operating System type
MESSAGE(STATUS "CMAKE_SYSTEM_NAME : ${CMAKE_SYSTEM_NAME}")
IF (CMAKE_SYSTEM_NAME MATCHES "Windows")
    ADD_DEFINITIONS( -D _WIN32 )
    ADD_DEFINITIONS( -D _CRT_SECURE_NO_WARNINGS )
    # ADD_DEFINITIONS( -D HAVE_VLD )
ELSE ()
    # For the other OS type: display fatal error and abort this cmake script.
    MESSAGE(FATAL_ERROR "UNIXem library is only supported on Windows OS platform.")
ENDIF (CMAKE_SYSTEM_NAME MATCHES "Windows")

SET(EXECUTABLE_OUTPUT_PATH  ${PROJECT_BINARY_DIR}/../bin)
SET(LIBRARY_OUTPUT_PATH     ${PROJECT_BINARY_DIR}/../lib)

# For Windows OS: Prompt to require CMAKE_BUILD_TYPE parameter in [Debug, Release]
IF (CMAKE_SYSTEM_NAME MATCHES "Windows")
    IF (CMAKE_BUILD_TYPE MATCHES Debug)
        MESSAGE( ">>> CMake in Debug mode! <<<" )
    ELSEIF (CMAKE_BUILD_TYPE MATCHES Release)
        MESSAGE( ">>> CMake in Release mode! <<<" )
    ELSE()
        MESSAGE( STATUS "=========================================================================" )
        MESSAGE( STATUS "Please provide CMAKE_BUILD_TYPE command line parameter." )
        MESSAGE( STATUS "For Example:" )
        MESSAGE( STATUS "--- For Debug ----" )
        MESSAGE( STATUS "    cmake -G \"Visual Studio 16 2019\" -A Win64 -D CMAKE_BUILD_TYPE=Debug ." )
        MESSAGE( STATUS "    cmake --build . --config Debug" )
        MESSAGE( STATUS "--- For Release ----" )
        MESSAGE( STATUS "    cmake -G \"Visual Studio 16 2019\" -A Win64 -D CMAKE_BUILD_TYPE=Release ." )
        MESSAGE( STATUS "    cmake --build . --config Release" )
        MESSAGE( STATUS "=========================================================================" )
        MESSAGE( FATAL_ERROR "" )
    ENDIF (CMAKE_BUILD_TYPE MATCHES Debug)
ENDIF (CMAKE_SYSTEM_NAME MATCHES "Windows")

# To Set the TargetDir variable
SET (EXE_TARGET_DIR ${EXECUTABLE_OUTPUT_PATH}/${CMAKE_BUILD_TYPE})
SET (LIB_TARGET_DIR ${LIBRARY_OUTPUT_PATH}/${CMAKE_BUILD_TYPE})
MESSAGE( STATUS "LIB_TARGET_DIR: " ${LIB_TARGET_DIR})

# TEST
# Link: https://cmake.org/cmake/help/v3.14/manual/cmake-variables.7.html
MESSAGE( STATUS "CMAKE_CONFIGURATION_TYPES: " ${CMAKE_CONFIGURATION_TYPES} )
MESSAGE( STATUS "CMAKE_GENERATOR: " ${CMAKE_GENERATOR} )
MESSAGE( STATUS "CMAKE_GENERATOR_PLATFORM: " ${CMAKE_GENERATOR_PLATFORM} )
MESSAGE( STATUS "CMAKE_VS_PLATFORM_NAME: " ${CMAKE_VS_PLATFORM_NAME} )
MESSAGE( STATUS "CMAKE_BUILD_TOOL: " ${CMAKE_BUILD_TOOL} )

INCLUDE_DIRECTORIES(
    ../../include
)

MESSAGE(STATUS "")
MESSAGE(STATUS "=========================================================")
MESSAGE(STATUS "| LibDev - Target UNIXem         (STATIC LIBRARY) BEGIN |")
MESSAGE(STATUS "=========================================================")
MESSAGE(STATUS "")

file(GLOB_RECURSE SRC_LIST_LIBDEV_UNIXem ../../src/*.c)

ADD_LIBRARY( unixem.core STATIC ${SRC_LIST_LIBDEV_UNIXem} )

MESSAGE(STATUS "")
MESSAGE(STATUS "=========================================================")
MESSAGE(STATUS "| LibDev - Target UNIXem         (STATIC LIBRARY) END   |")
MESSAGE(STATUS "=========================================================")
MESSAGE(STATUS "")
