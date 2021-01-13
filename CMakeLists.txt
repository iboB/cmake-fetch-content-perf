cmake_minimum_required(VERSION 3.14)

project(fc-perf)

macro(stamp text)
    if(WIN32)
        execute_process(COMMAND cmd /c echo %time% OUTPUT_VARIABLE ttt)
    else()
        execute_process(COMMAND date +"%T.%3N" OUTPUT_VARIABLE ttt)
    endif()

    message("${text} : ${ttt}")
endmacro()

include(FetchContent)

macro(dep name tag)
    stamp("${name} begin")
    FetchContent_Declare(
        ${name}
        GIT_REPOSITORY https://github.com/iboB/${name}.git
        GIT_TAG ${tag}
    )
    FetchContent_MakeAvailable(${name})
    stamp("${name} end")
endmacro()

dep(icm v1.2.0)
dep(doctest-lib e053b7ef07e79ac197d00136618690f92e0d84c4)

add_executable(scratch scratch.cpp)

