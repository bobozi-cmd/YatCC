file(GLOB _src *.cpp *.hpp *.c *.h)
add_executable(task3 ${_src})

target_include_directories(task3 PRIVATE ${LLVM_INCLUDE_DIRS})

target_link_libraries(task3 LLVM)
