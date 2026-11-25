cmake_minimum_required(VERSION 3.16)

project(geogram_delaunay LANGUAGES CXX)

find_package(Threads REQUIRED)

# Public inline arithmetic uses globals that are not exported by Windows DLLs.
add_library(geogram_delaunay STATIC Delaunay_psm.cpp Delaunay_psm.h)
add_library(geogram::delaunay ALIAS geogram_delaunay)

target_include_directories(geogram_delaunay PUBLIC "${CMAKE_CURRENT_SOURCE_DIR}")
target_link_libraries(geogram_delaunay PUBLIC Threads::Threads)
target_compile_features(geogram_delaunay PUBLIC cxx_std_17)
target_compile_definitions(geogram_delaunay PUBLIC GEO_STATIC_LIBS)

# Exact predicates, including inline code in the public header, must not
# contract multiply-add operations into FMAs.
if(MSVC)
    target_compile_options(geogram_delaunay PUBLIC /fp:strict)
elseif(CMAKE_CXX_COMPILER_ID MATCHES "^(GNU|Clang|AppleClang)$")
    target_compile_options(geogram_delaunay PUBLIC -ffp-contract=off)
endif()

add_executable(geogram_delaunay_example Delaunay_example.cpp)
target_link_libraries(geogram_delaunay_example PRIVATE geogram::delaunay)
