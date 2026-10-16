cmake_minimum_required(VERSION 3.20)
project(GTASymlinkGenerator LANGUAGES CXX)

if(WIN32)
    enable_language(RC)
endif()

add_executable(GTASymlinkGenerator
    "GTA Symlink Generator.cpp"
)

target_compile_features(GTASymlinkGenerator PRIVATE cxx_std_20)

if(WIN32)
    target_sources(GTASymlinkGenerator PRIVATE "GTA Symlink Generator.rc")
else()
    add_custom_command(TARGET GTASymlinkGenerator POST_BUILD
        COMMAND ${CMAKE_COMMAND} -E copy_directory
            "${CMAKE_CURRENT_SOURCE_DIR}/Languages"
            "$<TARGET_FILE_DIR:GTASymlinkGenerator>/Languages"
    )
endif()
