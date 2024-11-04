cmake_minimum_required(VERSION 3.27)

set(PROJECT_NAME OpenGLTutorial)
set(CMAKE_CXX_STANDARD 20)

# OpenGL Settings
set(WINDOW_NAME "Hello, OpenGL!")
set(WINDOW_WIDTH 640)
set(WINDOW_HEIGHT 480)

project(${PROJECT_NAME})
add_executable(${PROJECT_NAME} main.cpp)

set(GLAD glad)
include_directories(${CMAKE_CURRENT_SOURCE_DIR}/include)
add_library(glad ${CMAKE_CURRENT_SOURCE_DIR}/include/glad.c)

include(Dependency.cmake)

# 우리 프로젝트에 include / lib 관련 옵션 추가
target_include_directories(${PROJECT_NAME} PUBLIC ${DEP_INCLUDE_DIR})
target_link_directories(${PROJECT_NAME} PUBLIC ${DEP_LIB_DIR})
target_link_libraries(${PROJECT_NAME} PUBLIC ${DEP_LIBS})
target_link_libraries(${PROJECT_NAME} PUBLIC ${GLAD})

# 환경 변수를 predefined macro로 프로젝트에 추가
target_compile_definitions(${PROJECT_NAME} PUBLIC
        WINDOW_NAME="${WINDOW_NAME}"
        WINDOW_WIDTH=${WINDOW_WIDTH}
        WINDOW_HEIGHT=${WINDOW_HEIGHT}
)

# Dependency들이 먼저 build 될 수 있게 관계 설정
add_dependencies(${PROJECT_NAME} ${DEP_LIST})
