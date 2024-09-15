cmake_minimum_required(VERSION 3.16)
project(vulkanTest)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -lglfw -lvulkan -ldl -lpthread -lX11 -lXxf86vm -lXrandr -lXi")

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