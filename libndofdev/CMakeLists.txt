# -*- cmake -*-

cmake_minimum_required(VERSION 2.6)

project(libndofdev)

include_directories( include/ ../stage/packages/include )

SET(LIBRARY_OUTPUT_PATH "lib/release/" )
SET(EXECUTABLE_OUTPUT_PATH "bin" )

if (${CMAKE_SYSTEM_NAME} MATCHES "Linux")

    ADD_DEFINITIONS("-pipe -DUSE_SDL3")

    set(libndofdev_SOURCE_FILES
        ndofdev.c
    )

    set(libndofdev_HEADER_FILES
    	${CMAKE_CURRENT_SOURCE_DIR}/include/ndofdev_external.h
    )
    
elseif(${CMAKE_SYSTEM_NAME} MATCHES "Windows")
    message(FATAL_ERROR "Windows configuration not implemented. Use the 3DConnexion library located at http://bitbucket.org/lindenlab/3p-libndofdev  ") 
elseif(${CMAKE_SYSTEM_NAME} MATCHES "Darwin")
    message(FATAL_ERROR "Darwin configuration not implemented. Use the 3DConnexion library located at http://bitbucket.org/lindenlab/3p-libndofdev ") 
endif()

set_source_files_properties(${libndofdev_HEADER_FILES} PROPERTIES HEADER_FILE_ONLY TRUE)
list(APPEND libndofdev_SOURCE_FILES ${libndofdev_HEADER_FILES})

add_library (ndofdev_sdl3 STATIC ${libndofdev_SOURCE_FILES})

target_link_libraries(ndofdev_sdl3
    ${libndofdev_LIBRARIES}
)
