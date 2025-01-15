# Specify 'gcc' CXXCompilerID.
# set(CMAKE_MODULE_PATH).
# find_library(portaudio.h REQUIRED)
# set("portaudio.h"/${LIBRARY_DIR_PATH}).
# set(SOURCE_DIR_PATH="/home/wholesomedegenerate/ai_spotibot_player")
# set(BUILD_DIR_PATH="/home/wholesomedegenerate/ai_spotibot_player/build")

# Minimum required version
cmake_minimum_required(VERSION 3.25.1)
project(<AI_SPOTIBOT_PLAYER> LANGUAGES C CXX)

# C++ standard
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# Specifies path to static project source and build directories
set(SOURCE_DIR="/home/wholesomedegenerate/ai_spotibot_player")
set(BUILD_DIR="/home/wholesomedegenerate/ai_spotibot_player/build")

# Set compiler
set(CMAKE_C_COMPILER gcc)
set(CMAKE_CXX_COMPILER g++)

# Set the MODULE PATH
set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} "/home/wholesomedegenerate/.local/lib/python3.11/site-packages/cmake_modules")

# Find PortAudio
find_path(PORTAUDIO_INCLUDE_DIR portaudio.h)
find_library(PORTAUDIO_LIBRARY NAMES portaudio PATHS ${ADD_THIRDPARTY_LIB})

if(NOT PORTAUDIO_INCLUDE_DIR OR NOT PORTAUDIO_LIBRARY)
        message(FATAL_ERROR "PortAudio not found. Please install portaudio19-dev or set PORTAUDIO_INCLUDE_DIR and PORTAUDIO_LIBRARY manually.")
endif()

include_directories(${PORTAUDIO_INCLUDE_DIR})
link_libraries(${PORTAUDIO_LIBRARY})

# Sets paths to libraries 
set(ARROW_LIBRARY_PATH_SUFFIXES
	"/usr"
	"/usr/.local"
	"/usr/include"
	"lib"
	"python3.11/site-packages/cmake_modules"
)
set(ARROW_INCLUDE_PATH_SUFFIXES
	"include"
	"lib"
	"Library"
	"Library/include"
)
set(ADD_THIRDPARTY_LIB
	"/usr"
	"/usr/.local"
	"/usr/myenv"
	"/usr/include"
	"python3.11/site-packages/pyaudio"
	"python3.11/site-packages/pyaudio/__pycache__"
	"lib64"
	"lib"
	"/usr/include/portaudio.h"
	"/usr/lib/x86_64-linux-gnu/libportaudio.so"
)

include_directories(${ARROW_INCLUDE_PATH_SUFFIXES})
include_directories("/usr/include/portaudio")

link_directories(${ARROW_LIBRARY_PATH_SUFFIXES})
link_directories("/usr/lib")

# Find Packages
find_package(Cython REQUIRED)
include_directories(${CYTHON_INCLUDE_DIRS})
find_package(Python 3.11 REQUIRED)
include_directories(${PYTHON3.11_INCLUDE_DIRS})

