cmake_minimum_required(VERSION 3.0.0)
project(QtPropertyBrowser VERSION 0.1.0)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)


find_package(Qt6 COMPONENTS Widgets REQUIRED)
qt_standard_project_setup()

set(HEADER_FILES
    include/qtbuttonpropertybrowser.h
    include/qteditorfactory.h
    include/qtgroupboxpropertybrowser.h
    include/qtpropertybrowser.h
    include/qtpropertybrowserutils_p.h
    include/qtpropertymanager.h
    include/qttreepropertybrowser.h
    include/qtvariantproperty.h
)


set(SOURCE_FILES
    src/qtbuttonpropertybrowser.cpp 
    src/qteditorfactory.cpp
    src/qtgroupboxpropertybrowser.cpp 
    src/qtpropertybrowser.cpp 
    src/qtpropertybrowserutils.cpp 
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


qt_add_library(QtPropertyBrowser  ${SOURCE_FILES} ${HEADER_FILES})
target_link_libraries(QtPropertyBrowser PUBLIC Qt6::Widgets)
target_include_directories(QtPropertyBrowser PUBLIC include)


qt_add_resources(QtPropertyBrowser qtpropertybrowser
    PREFIX "/qt-project.org/qtpropertybrowser/"
    FILES ${RESOURCE_FILES}
)

set_target_properties(QtPropertyBrowser PROPERTIES
    AUTOMOC ON
    AUTORCC ON
    CXX_EXTENSIONS OFF
    VERSION ${VERSION_SHORT}
    EXPORT_NAME ${library_name}
    ARCHIVE_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/lib"
    LIBRARY_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/lib"
    RUNTIME_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/bin"
)
set_target_properties(QtPropertyBrowser PROPERTIES
    CXX_STANDARD 17
    CXX_STANDARD_REQUIRED ON)


include(CMakePackageConfigHelpers)
write_basic_package_version_file(
    "QtPropertyBrowserConfigVersion.cmake"
    VERSION 6.5.1
    COMPATIBILITY SameMajorVersion
)
install(FILES ${HEADER_FILES}
    DESTINATION include/
    COMPONENT headers
)

install(TARGETS QtPropertyBrowser
    EXPORT QtPropertyBrowserTargets
    RUNTIME DESTINATION bin
    LIBRARY DESTINATION lib
    ARCHIVE DESTINATION lib
    INCLUDES DESTINATION include
)

# install(EXPORT QtPropertyBrowserTargets
#     FILE QtPropertyBrowserTargets.cmake
#     NAMESPACE QtPropertyBrowserTargets::
#     DESTINATION lib/cmake/QtPropertyBrowserTargets
# )
# install(FILES QtPropertyBrowserTargetsConfig.cmake RENAME QtPropertyBrowserConfig.cmake
#     DESTINATION lib/cmake/QtPropertyBrowserTargets
# )
# install(FILES "${CMAKE_CURRENT_BINARY_DIR}/QtPropertyBrowserConfigVersion.cmake"
#     DESTINATION lib/cmake/QtPropertyBrowser
# )

target_include_directories(QtPropertyBrowser PUBLIC
    $<INSTALL_INTERFACE:include>
    $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}>
)

