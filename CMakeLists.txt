cmake_minimum_required(VERSION 3.20)

# Define project name, version, and language
project(JAAG VERSION 1.0.0 LANGUAGES CXX)

# Enforce C++23 globally for consumers/builds
set(CMAKE_CXX_STANDARD 23)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_EXTENSIONS OFF)

# Create an INTERFACE (header-only) target
add_library(jaag INTERFACE)

# Define namespaced alias for target_link_libraries(myapp PRIVATE jaag::jaag)
add_library(jaag::jaag ALIAS jaag)

# Define include directories for build tree and install tree
target_include_directories(jaag INTERFACE
	$<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include>
	$<INSTALL_INTERFACE:include>
)

# Enforce C++23 standard requirement on the INTERFACE target
target_compile_features(jaag INTERFACE cxx_std_20) # Ensures minimum C++20 compiler support
set_target_properties(jaag PROPERTIES INTERFACE_CXX_STANDARD 23)

