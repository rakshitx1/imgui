# Define minimum CMake version
cmake_minimum_required(VERSION 3.20)

# Define project and languages
project(ImGui CXX)

# List of ImGui source files
set(IMGUI_SOURCES
  imgui.cpp
  imgui_draw.cpp
  imgui_widgets.cpp
  imgui_demo.cpp
  imgui_tables.cpp
)

# List of ImGui header files
set(IMGUI_HEADERS
  imgui.h
  imconfig.h
  imgui_internal.h
  imstb_rectpack.h
  imstb_textedit.h
  imstb_truetype.h
)

# Add backend implementation files
set(IMGUI_BACKEND_SOURCES
  backends/imgui_impl_glfw.cpp
  backends/imgui_impl_opengl3.cpp
)

# Add ImGui library target
add_library(ImGui ${IMGUI_SOURCES} ${IMGUI_HEADERS} ${IMGUI_BACKEND_SOURCES})

# Include directories for ImGui
target_include_directories(ImGui PUBLIC 
  ${CMAKE_CURRENT_SOURCE_DIR}
  ${CMAKE_CURRENT_SOURCE_DIR}/backends
  ${CMAKE_CURRENT_SOURCE_DIR}/Vendor/GLFW/include # Include GLFW headers
)

# Find OpenGL package
find_package(OpenGL REQUIRED)

# Include OpenGL directories
target_include_directories(ImGui PUBLIC ${OPENGL_INCLUDE_DIR})

# Link OpenGL libraries
target_link_libraries(ImGui PUBLIC ${OPENGL_gl_LIBRARY})

# Link GLFW libraries (already linked in Ember project, ensure it's available)
target_link_libraries(ImGui PUBLIC glfw)

# Set compiler options
target_compile_features(ImGui PUBLIC cxx_std_17)
