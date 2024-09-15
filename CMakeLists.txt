cmake_minimum_required(VERSION 3.16)
project(vulkanTest)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -lglfw -lvulkan -ldl -lpthread -lX11 -lXxf86vm -lXrandr -lXi")
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}/bin)

# set_target_properties(${project} PROPERTIES RUNTIME_OUTPUT_DIRECTORY_DEBUG "${${CMAKE_CURRENT_SOURCE_DIR}/bin}")
# set_target_properties(${project} PROPERTIES RUNTIME_OUTPUT_DIRECTORY "${${CMAKE_CURRENT_SOURCE_DIR}/bin}")
# set_target_properties(${project} PROPERTIES RUNTIME_OUTPUT_DIRECTORY_RELEASE "${${CMAKE_CURRENT_SOURCE_DIR}/bin}")
# set_target_properties(${project} PROPERTIES RUNTIME_OUTPUT_DIRECTORY_RELWITHDEBINFO "${${CMAKE_CURRENT_SOURCE_DIR}/bin}")

ADD_LIBRARY(LibsModule 
    main.cpp
)
target_link_libraries(LibsModule -lglfw -lvulkan -ldl -lpthread -lX11 -lXxf86vm -lXrandr -lXi)
target_link_libraries(LibsModule -L/usr/lib/x86_64-linux-gnu/)


add_executable(vulkanTest main.cpp)
target_link_libraries(vulkanTest LibsModule)

find_package(Vulkan REQUIRED)
target_include_directories(${PROJECT_NAME} PUBLIC ${Vulkan_INCLUDE_DIRS})
target_link_libraries(${PROJECT_NAME} Vulkan::Vulkan)

# find_package(PkgConfig REQUIRED)
# pkg_search_module(GLM REQUIRED glm)
# include_directories(${GLM_INCLUDE_DIRS})
# target_link_libraries(${PROJECT_NAME} ${GLM_LIBRARY_DIRS})

find_package(glfw3 3.2 REQUIRED)
include_directories(${GLFW_INCLUDE_DIRS})
target_link_libraries(${PROJECT_NAME} ${GLFW_LIBRARIES})

# # change output directory
# function(set_binary_dir project)
# 	set_target_properties(${project} PROPERTIES RUNTIME_OUTPUT_DIRECTORY "${COMPUTE_BINARY_DIR}")
# 	set_target_properties(${project} PROPERTIES RUNTIME_OUTPUT_DIRECTORY_DEBUG "${COMPUTE_BINARY_DIR}")
# 	set_target_properties(${project} PROPERTIES RUNTIME_OUTPUT_DIRECTORY_RELEASE "${COMPUTE_BINARY_DIR}")
# 	set_target_properties(${project} PROPERTIES RUNTIME_OUTPUT_DIRECTORY_RELWITHDEBINFO "${COMPUTE_BINARY_DIR}")
# 	set_target_properties(${project} PROPERTIES VS_DEBUGGER_WORKING_DIRECTORY "${COMPUTE_BINARY_DIR}")
# endfunction()

