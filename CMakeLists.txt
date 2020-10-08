cmake_minimum_required(VERSION 3.10)

macro(print_all_variables)
    message(STATUS "print_all_variables------------------------------------------{")
    get_cmake_property(_variableNames VARIABLES)
    foreach (_variableName ${_variableNames})
        message(STATUS "${_variableName}=${${_variableName}}")
    endforeach()
    message(STATUS "print_all_variables------------------------------------------}")
endmacro()

# set the project name
project(ffmpegtutorial)

include_directories(include /usr/local/include)
link_directories(/usr/local/lib)

set(LIBAV_LIBS  libavcodec.58.dylib 
                libavformat.58.dylib 
                libavutil.56.dylib 
                libavresample.4.dylib 
                libavdevice.58.dylib
                libavfilter.7.dylib
                libswscale.5.dylib
                libswresample.3.dylib)

# add the executable
add_executable(decoder src/decoder.cpp)
target_link_libraries(decoder ${LIBAV_LIBS})

add_custom_target(run
    COMMAND decoder
    DEPENDS decoder
    WORKING_DIRECTORY ${CMAKE_PROJECT_DIR}
)
