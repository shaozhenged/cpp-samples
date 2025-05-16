cmake_minimum_required(VERSION 3.14)
project(pluxbiosignals-sample LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

# 检测操作系统
if(WIN32)
    # Windows系统
    if(CMAKE_SIZEOF_VOID_P EQUAL 8)
        # 64-bit
        message(STATUS "Configuring for 64-bit Windows")
        set(PLUX_LIBS ${CMAKE_CURRENT_SOURCE_DIR}/lib/plux64.lib
                      ${CMAKE_CURRENT_SOURCE_DIR}/LibFT4222-64.dll
                      ${CMAKE_CURRENT_SOURCE_DIR}/LibFT4222AB-64.dll)
    else()
        # 32-bit
        message(STATUS "Configuring for 32-bit Windows")
        set(PLUX_LIBS ${CMAKE_CURRENT_SOURCE_DIR}/lib/plux.lib
                      ${CMAKE_CURRENT_SOURCE_DIR}/LibFT4222.dll
                      ${CMAKE_CURRENT_SOURCE_DIR}/LibFT4222AB.dll)
    endif()
elseif(APPLE)
    # macOS系统
    message(STATUS "Configuring for macOS")
    set(PLUX_LIBS ${CMAKE_CURRENT_SOURCE_DIR}/lib/libplux.a)
elseif(UNIX AND NOT APPLE)
    # Linux系统
    message(STATUS "Configuring for Linux")
    set(PLUX_LIBS ${CMAKE_CURRENT_SOURCE_DIR}/lib/libplux.a)
else()
    message(FATAL_ERROR "Unsupported operating system")
endif()

# 源文件
set(SOURCES
    simpleApp.cpp
    simpleDev.cpp
)

# 头文件
set(HEADERS
    plux.h
    simpleDev.h
)

# 创建可执行文件
add_executable(${PROJECT_NAME} ${SOURCES} ${HEADERS})

# 包含目录
target_include_directories(${PROJECT_NAME} PRIVATE ${CMAKE_CURRENT_SOURCE_DIR})

# 链接库
target_link_libraries(${PROJECT_NAME} PRIVATE ${PLUX_LIBS})

# 设置属性使其可以在Qt Creator中使用
set(CMAKE_AUTOUIC ON)
set(CMAKE_AUTOMOC ON)
set(CMAKE_AUTORCC ON)

# 如果需要Qt组件，取消下面的注释（目前这个项目不需要Qt）
# find_package(QT NAMES Qt6 Qt5 REQUIRED COMPONENTS Core)
# find_package(Qt${QT_VERSION_MAJOR} REQUIRED COMPONENTS Core)
# target_link_libraries(${PROJECT_NAME} PRIVATE Qt${QT_VERSION_MAJOR}::Core) 