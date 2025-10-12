cmake_minimum_required(VERSION 3.26.4)

project(ImGuiColorTextEdit LANGUAGES CXX)
set(CMAKE_CXX_STANDARD 23)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

add_library(ImGuiColorTextEdit "LanguageDefinitions.cpp" "TextEditor.cpp" "UnitTests.cpp")

target_include_directories(ImGuiColorTextEdit PUBLIC ..)

find_package(imgui CONFIG REQUIRED)
target_link_libraries(ImGuiColorTextEdit PUBLIC imgui::imgui)

# Disable all warnings - ImGuiColorTextEdit is external library
if (MSVC)
    target_compile_options(ImGuiColorTextEdit PRIVATE /W0)
elseif ("${CMAKE_CXX_COMPILER_ID}" STREQUAL "GNU")
    target_compile_options(ImGuiColorTextEdit PRIVATE -w)
elseif ("${CMAKE_CXX_COMPILER_ID}" STREQUAL "Clang")
    target_compile_options(ImGuiColorTextEdit PRIVATE -w)
endif()