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


qt_add_library(QtPropertyBrowser STATIC ${SOURCE_FILES} ${HEADER_FILES})
target_link_libraries(QtPropertyBrowser PUBLIC Qt6::Widgets)
target_include_directories(QtPropertyBrowser PUBLIC include)


qt_add_resources(QtPropertyBrowser qtpropertybrowser
    PREFIX "/qt-project.org/qtpropertybrowser/"
    FILES ${RESOURCE_FILES}
)
