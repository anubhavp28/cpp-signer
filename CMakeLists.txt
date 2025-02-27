
include(FetchContent)

cmake_minimum_required (VERSION 3.10)

# This is your project statement. You should always list languages;
# Listing the version is nice here since it sets lots of useful variables
project(
  eosio_r1_key
  VERSION 1.0
  LANGUAGES CXX)

if (APPLE)
set(OPENSSL_ROOT_DIR "/usr/local/opt/openssl@1.1")
endif()
find_package(OpenSSL 1.1 REQUIRED)
set(CMAKE_CXX_STANDARD 17)

set(ABIEOS_BUILD_SHARED_LIB OFF)
FetchContent_Declare(
  abieos
  GIT_REPOSITORY https://github.com/EOSIO/abieos.git
  GIT_TAG 92920886a9c8606fbda5bbdca41365f4e617e37e
)
FetchContent_MakeAvailable(abieos)

add_subdirectory(src)

option(EOSIO_R1_KEY_ENABLE_TEST "Enable building test" OFF)
option(EOSIO_R1_KEY_ENABLE_EXAMPLE "Enable building example" OFF)

if (EOSIO_R1_KEY_ENABLE_TEST)
enable_testing()
add_subdirectory(tests)
endif()

if (EOSIO_R1_KEY_ENABLE_EXAMPLE)
add_subdirectory(example)
endif()