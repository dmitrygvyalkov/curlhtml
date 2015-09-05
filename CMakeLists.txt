cmake_minimum_required(VERSION 2.8) # Проверка версии CMake.
                                    # Если версия установленой программы
                                    # старее указаной, произайдёт аварийный выход.

project(htmltitle)				# Название проекта

set(SOURCE_EXE htmltitle.cpp)			# Установка переменной со списком исходников
add_executable(htmltitle ${SOURCE_EXE})


#set(CMAKE_MODULE_PATH ${CMAKE_CURRENT_SOURCE_DIR}/cmake)
#message(STATUS "Use Cmake Mudele Dir: " ${CMAKE_MODULE_PATH} )

##########################################################
find_package(LibXml2 REQUIRED)
if(NOT LIBXML2_FOUND)
    message(SEND_ERROR "Failed to find LibXml2")
    return()
else()
    message(STATUS "LibXml2: Ok " ${LIBXML2_INCLUDE_DIR} )
    #set ( LIBXML2_INCLUDE_DIRS " /usr/local/include/libxml2/" )
    #message(STATUS ${LIBXML2_INCLUDE_DIRS})
    include_directories(${LIBXML2_INCLUDE_DIR})
endif()

find_package(CURL REQUIRED)
message(STATUS "Curl: Ok " ${CURL_INCLUDE_DIRS})
include_directories(${CURL_INCLUDE_DIRS})
target_link_libraries(${CURL_LIBRARIES})
##########################################################
target_link_libraries( htmltitle
                                ${LIBXML2_LIBRARIES}
                                ${CURL_LIBRARIES})

#add_executable(htmltitle ${SOURCE_EXE})	# Создает исполняемый файл с именем main

include(CPack) 