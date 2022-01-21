cmake_minimum_required(VERSION 3.5)

set(TARGET WebKit2Gtk)

project(${TARGET} LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

add_executable(${TARGET} main.cpp)

find_package(PkgConfig REQUIRED)

set(LIBS_LIST gtk+-3.0 webkit2gtk-4.0)
foreach(LIB IN LISTS LIBS_LIST)
    pkg_check_modules(${LIB} REQUIRED ${LIB})
    target_link_libraries(${TARGET} ${${LIB}_LIBRARIES})
    target_include_directories(${TARGET} PUBLIC ${${LIB}_INCLUDE_DIRS})
    target_compile_options(${TARGET} PUBLIC ${${LIB}_CFLAGS_OTHER})
endforeach()



