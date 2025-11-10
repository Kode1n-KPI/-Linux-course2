cmake_minimum_required(VERSION 3.10)

project(CalculatorProject VERSION 1.0)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED True)

# 1. Оголошення бібліотеки
add_library(math SHARED math_functions.cpp)

# 2. Оголошення виконуваного файлу
add_executable(app main.cpp)

target_include_directories(math PUBLIC ${CMAKE_CURRENT_SOURCE_DIR})

# 3. КОРЕКЦІЯ: Явно вказуємо, що це консольна програма. 
# Це правильний спосіб вирішення проблеми 'WinMain' у MinGW/CMake.
set_target_properties(app PROPERTIES LINK_FLAGS "-Wl,--subsystem,console")

# 4. Компонування
target_link_libraries(app PRIVATE math)
