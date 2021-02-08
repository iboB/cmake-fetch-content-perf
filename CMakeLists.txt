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

# set(FETCHCONTENT_QUIET NO)

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

dep(doctest-lib e053b7ef07e79ac197d00136618690f92e0d84c4)
dep(icm v1.2.0)
dep(dynamix f447868c90f0142dcb3c9b072018b2f2911e2008)
dep(confy 0b5951a4655924aea2f7fb48b902830237627802)
dep(itlib v1.2.2)
dep(splat v1.0.0)
dep(kuzco v1.3.0)

add_executable(scratch scratch.cpp)

