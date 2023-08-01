cmake_minimum_required(VERSION 3.0.0)
project(QtPropertyBrowser VERSION 0.1.0)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)


find_package(Qt6 COMPONENTS Widgets REQUIRED)
qt_standard_project_setup()

set(HEADER_FILES
    qtbuttonpropertybrowser.h
    qteditorfactory.h
    qtgroupboxpropertybrowser.h
    qtpropertybrowser.h
    qtpropertybrowserutils_p.h
    qtpropertymanager.h
    qttreepropertybrowser.h
    qtvariantproperty.h
)


set(SOURCE_FILES
    qtbuttonpropertybrowser.cpp 
    qteditorfactory.cpp
    qtgroupboxpropertybrowser.cpp 
    qtpropertybrowser.cpp 
    qtpropertybrowserutils.cpp 
    qtpropertymanager.cpp 
    qttreepropertybrowser.cpp 
    qtvariantproperty.cpp 
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
target_link_libraries(QtPropertyBrowser PRIVATE Qt6::Widgets)


qt_add_resources(QtPropertyBrowser qtpropertybrowser
    PREFIX "/qt-project.org/qtpropertybrowser/"
    FILES ${RESOURCE_FILES}
)
