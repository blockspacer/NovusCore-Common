project(common VERSION 1.0.0 DESCRIPTION "Common is a static library for NovusCore")

add_subdirectory(Dependencies)
file(GLOB_RECURSE COMMON_FILES "*.cpp" "*.h")

add_library(${PROJECT_NAME} ${COMMON_FILES})
add_library(${PROJECT_NAME}::${PROJECT_NAME} ALIAS ${PROJECT_NAME})
set_target_properties(${PROJECT_NAME} PROPERTIES FOLDER ${ROOT_FOLDER}/libs)

find_assign_files(${COMMON_FILES})

target_include_directories(${PROJECT_NAME} PUBLIC ${CMAKE_CURRENT_SOURCE_DIR})
target_link_libraries(${PROJECT_NAME} PUBLIC
    tracy::tracy
    common::dependencies
    openssl::openssl
    type_safe::type_safe
)

add_compile_definitions(NOMINMAX _SILENCE_ALL_CXX17_DEPRECATION_WARNINGS)