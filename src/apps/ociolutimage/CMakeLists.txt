if (OIIO_FOUND)
    include_directories(
        ${CMAKE_SOURCE_DIR}/export/
        ${CMAKE_BINARY_DIR}/export/
        ${CMAKE_SOURCE_DIR}/src/apps/share/
        ${OIIO_INCLUDES}
        ${ILMBASE_INCLUDES}
    )
    
    file(GLOB_RECURSE share_src_files "${CMAKE_SOURCE_DIR}/src/apps/share/*.cpp")
    
    add_executable(ociolutimage ${share_src_files} main.cpp)
    
    set_target_properties(ociolutimage PROPERTIES COMPILE_FLAGS -DCMAKE_BUILD_TYPE=${CMAKE_BUILD_TYPE})

    target_link_libraries(ociolutimage ${OIIO_LIBRARIES} ${CMAKE_DL_LIBS})
    
    target_link_OCIO(ociolutimage)
    
    install(TARGETS ociolutimage EXPORT OpenColorIO DESTINATION ${CMAKE_INSTALL_EXEC_PREFIX}/bin)
endif()
