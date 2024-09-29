cmake_minimum_required(VERSION 3.20)

project(ImGui LANGUAGES CXX)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

set(IMGUI_SOURCES
    imgui.cpp
    imgui_draw.cpp
    imgui_demo.cpp
    imgui_tables.cpp
    imgui_widgets.cpp
    backends/imgui_impl_opengl3.cpp
    backends/imgui_impl_glfw.cpp
)

set(IMGUI_HEADERS
    imgui.h
    imconfig.h
    imgui_internal.h
    imstb_rectpack.h
    imstb_textedit.h
    imstb_truetype.h
)

add_library(ImGui STATIC ${IMGUI_SOURCES} ${IMGUI_HEADERS})

target_include_directories(ImGui PUBLIC ${CMAKE_CURRENT_SOURCE_DIR})

if(WIN32)
    target_compile_definitions(ImGui PRIVATE "IMGUI_IMPL_WIN32")
    set(CMAKE_SYSTEM_VERSION "latest")
elseif(UNIX)
    target_compile_options(ImGui PRIVATE -fPIC)
    set(CMAKE_SYSTEM_VERSION "latest")
endif()

find_package(OpenGL REQUIRED)
find_package(glfw3 REQUIRED)

target_link_libraries(ImGui PRIVATE glfw OpenGL::GL)
