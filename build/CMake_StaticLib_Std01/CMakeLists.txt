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
    MESSAGE(FATAL_ERROR "UNIXem library is only supported on Windows (WIN32) OS platform.")
ENDIF (CMAKE_SYSTEM_NAME MATCHES "Windows")

