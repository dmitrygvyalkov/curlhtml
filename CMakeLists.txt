cmake_minimum_required(VERSION 2.8)

project(htmltitle)

set(SOURCE_EXE htmltitle.cpp)
add_executable(htmltitle ${SOURCE_EXE})

##########################################################
find_package(LibXml2 REQUIRED)
if(NOT LIBXML2_FOUND)
    message(SEND_ERROR "Failed to find LibXml2")
    return()
else()
    message(STATUS "LibXml2: Ok " ${LIBXML2_INCLUDE_DIRS} )
    #set ( LIBXML2_INCLUDE_DIRS " /usr/local/include/libxml2/" )
    #message(STATUS ${LIBXML2_INCLUDE_DIRS})
    include_directories(${LIBXML2_INCLUDE_DIRS})
endif()

find_package(CURL REQUIRED)
message(STATUS "Curl: Ok " ${CURL_INCLUDE_DIRS})
include_directories(${CURL_INCLUDE_DIRS})
target_link_libraries(${CURL_LIBRARIES})
##########################################################
target_link_libraries( htmltitle
                                ${LIBXML2_LIBRARIES}
                                ${CURL_LIBRARIES})

include(CPack) 