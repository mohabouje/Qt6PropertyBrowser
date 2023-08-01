cmake_minimum_required(VERSION 3.0.0)
project(qtpropertybrowser VERSION 6.5.1)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

option(QTPPROPERTYBROWSER_BUILD_SHARED_LIBS "Build shared libraries" ON)

find_package(Qt6 COMPONENTS Widgets REQUIRED)
qt_standard_project_setup()

set(HEADER_FILES
    include/${PROJECT_NAME}/qtbuttonpropertybrowser.h
    include/${PROJECT_NAME}/qteditorfactory.h
    include/${PROJECT_NAME}/qtgroupboxpropertybrowser.h
    include/${PROJECT_NAME}/${PROJECT_NAME}.h
    include/${PROJECT_NAME}/${PROJECT_NAME}utils_p.h
    include/${PROJECT_NAME}/qtpropertymanager.h
    include/${PROJECT_NAME}/qttreepropertybrowser.h
    include/${PROJECT_NAME}/qtvariantproperty.h
)


set(SOURCE_FILES
    src/qtbuttonpropertybrowser.cpp 
    src/qteditorfactory.cpp
    src/qtgroupboxpropertybrowser.cpp 
    src/${PROJECT_NAME}.cpp 
    src/${PROJECT_NAME}utils.cpp 
    src/qtpropertymanager.cpp 
    src/qttreepropertybrowser.cpp 
    src/qtvariantproperty.cpp 
)

set(RESOURCE_FILES
    "images/cursor-arrow.png"
    "images/cursor-busy.png"
    "images/cursor-closedhand.png"
    "images/cursor-cross.png"
    "images/cursor-forbidden.png"
    "images/cursor-hand.png"
    "images/cursor-hsplit.png"
    "images/cursor-ibeam.png"
    "images/cursor-openhand.png"
    "images/cursor-sizeall.png"
    "images/cursor-sizeb.png"
    "images/cursor-sizef.png"
    "images/cursor-sizeh.png"
    "images/cursor-sizev.png"
    "images/cursor-uparrow.png"
    "images/cursor-vsplit.png"
    "images/cursor-wait.png"
    "images/cursor-whatsthis.png"
)

set(VERSION_SHORT "${PROJECT_VERSION_MAJOR}.${PROJECT_VERSION_MINOR}.${PROJECT_VERSION_PATCH}")

if (QTPPROPERTYBROWSER_BUILD_SHARED_LIBS)
    qt_add_library(${PROJECT_NAME} ${SOURCE_FILES} ${HEADER_FILES})
else()
    qt_add_library(${PROJECT_NAME} STATIC ${SOURCE_FILES} ${HEADER_FILES})
endif()

target_link_libraries(${PROJECT_NAME} PUBLIC Qt6::Widgets)
target_include_directories(${PROJECT_NAME} PRIVATE include)


qt_add_resources(${PROJECT_NAME} ${PROJECT_NAME}
    PREFIX "/qt-project.org/${PROJECT_NAME}/"
    FILES ${RESOURCE_FILES}
)

set_target_properties(${PROJECT_NAME} PROPERTIES
    AUTOMOC ON
    AUTORCC ON
    CXX_EXTENSIONS OFF
    EXPORT_NAME ${PROJECT_NAME}
    VERSION ${VERSION_SHORT}
    ARCHIVE_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/lib"
    LIBRARY_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/lib"
    RUNTIME_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/bin"
)
set_target_properties(${PROJECT_NAME} PROPERTIES
    CXX_STANDARD 17
    CXX_STANDARD_REQUIRED ON)


include(CMakePackageConfigHelpers)
write_basic_package_version_file(
    "${PROJECT_NAME}ConfigVersion.cmake"
    VERSION ${VERSION_SHORT}
    COMPATIBILITY SameMajorVersion
)
install(FILES ${HEADER_FILES}
    DESTINATION include/${PROJECT_NAME}
    COMPONENT headers
)

install(TARGETS ${PROJECT_NAME}
    EXPORT ${PROJECT_NAME}Targets
    RUNTIME DESTINATION bin
    LIBRARY DESTINATION lib
    ARCHIVE DESTINATION lib
    INCLUDES DESTINATION include/${PROJECT_NAME}
)

install(EXPORT ${PROJECT_NAME}Targets
    FILE ${PROJECT_NAME}Targets.cmake
    NAMESPACE ${PROJECT_NAME}::
    DESTINATION lib/cmake/${PROJECT_NAME}
)

install(FILES ${PROJECT_NAME}Config.cmake RENAME ${PROJECT_NAME}Config.cmake
    DESTINATION lib/cmake/${PROJECT_NAME}
)

install(FILES "${CMAKE_CURRENT_BINARY_DIR}/${PROJECT_NAME}ConfigVersion.cmake"
    DESTINATION lib/cmake/${PROJECT_NAME}
)

target_include_directories(${PROJECT_NAME} PUBLIC
    $<INSTALL_INTERFACE:include>
    $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}>
)