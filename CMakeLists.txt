cmake_minimum_required(VERSION 4.2)

project(m6502 C)


set(target m6502)
add_library(${target} STATIC
    m6502.c
    m6502.h
)

set(target m6502_tests)
add_executable(${target}
    m6502_tests.c
)
target_link_libraries(${target} PRIVATE m6502)

# copy programs

add_custom_command(TARGET ${target} POST_BUILD
    COMMAND ${CMAKE_COMMAND} -E copy_directory 
        ${CMAKE_CURRENT_SOURCE_DIR}/programs
        $<TARGET_FILE_DIR:${target}>/programs)