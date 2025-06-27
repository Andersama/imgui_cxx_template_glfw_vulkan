# glfw3
find_package(glfw3 REQUIRED)
include_directories(${GLFW_INCLUDE_DIRS})

#vulkan
find_package(Vulkan REQUIRED)

set(IMGUI_DIR "imgui")
message(STATUS "IMGUI_DIR: ${IMGUI_DIR}")
include_directories(${GLFW_DIR}/deps ${IMGUI_DIR} ${IMGUI_DIR}/backends)

# Add source to this project's executable.
add_executable (${PROJECT_NAME} "imgui_cxx_vulkan.cpp" "imgui_cxx_vulkan.h"
	${IMGUI_DIR}/backends/imgui_impl_glfw.cpp ${IMGUI_DIR}/backends/imgui_impl_vulkan.cpp ${IMGUI_DIR}/imgui.cpp ${IMGUI_DIR}/imgui_draw.cpp ${IMGUI_DIR}/imgui_demo.cpp ${IMGUI_DIR}/imgui_tables.cpp ${IMGUI_DIR}/imgui_widgets.cpp
)

if (CMAKE_VERSION VERSION_GREATER 3.12)
  set_property(TARGET ${PROJECT_NAME} PROPERTY CXX_STANDARD 20)
endif()

# TODO: Add tests and install targets if needed.

target_link_libraries(${PROJECT_NAME} PRIVATE
	glfw
	Vulkan::Vulkan
)
