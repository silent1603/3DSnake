cmake_minimum_required(VERSION 3.13)


project(3DSnake)

find_package(EASTL CONFIG REQUIRED)
find_package(spdlog CONFIG REQUIRED)
find_package(glm CONFIG REQUIRED)
find_package(assimp CONFIG REQUIRED)
find_package(Freetype REQUIRED)
find_package(Bullet CONFIG REQUIRED)
find_package(assimp CONFIG REQUIRED)
find_package(nlohmann_json CONFIG REQUIRED)
find_package(SDL2_image CONFIG REQUIRED)
find_package(SDL2_mixer CONFIG REQUIRED)
find_package(SDL2_ttf CONFIG REQUIRED)
find_package(SDL2 CONFIG REQUIRED)
find_package(EnTT CONFIG REQUIRED)
find_package(glad CONFIG REQUIRED)
find_package(OpenAL CONFIG REQUIRED) 
find_package(imgui CONFIG REQUIRED)
find_path(STB_INCLUDE_DIRS "stb_c_lexer.h")

set(nlohmann-json_IMPLICIT_CONVERSIONS OFF)

set(SRC_PATH ${CMAKE_CURRENT_SOURCE_DIR})

file(GLOB_RECURSE PROJECT_SOURCES ${SRC_PATH}/*.cpp)
file(GLOB_RECURSE PROJECT_HEADERS ${SRC_PATH}/*.h)

source_group(TREE ${PROJECT_PATH} FILES ${PROJECT_SOURCES})
source_group(TREE ${PROJECT_PATH} FILES ${PROJECT_HEADERS})

add_library(3DSnake SHARED ${PROJECT_HEADERS} ${PROJECT_SOURCES})

set_property(TARGET 3DSnake PROPERTY CXX_STANDARD 11)

target_include_directories(3DSnake PRIVATE ${STB_INCLUDE_DIRS} 
                                    PRIVATE ${CMAKE_CURRENT_SOURCE_DIR}) 

target_link_libraries(3DSnake PRIVATE $<TARGET_NAME_IF_EXISTS:SDL2::SDL2main> 
                                        PRIVATE $<IF:$<TARGET_EXISTS:SDL2::SDL2>,SDL2::SDL2,SDL2::SDL2-static>  
                                        PRIVATE $<IF:$<TARGET_EXISTS:SDL2_image::SDL2_image>,SDL2_image::SDL2_image,SDL2_image::SDL2_image-static> 
                                        PRIVATE $<IF:$<TARGET_EXISTS:SDL2_mixer::SDL2_mixer>,SDL2_mixer::SDL2_mixer,SDL2_mixer::SDL2_mixer-static> 
                                        PRIVATE $<IF:$<TARGET_EXISTS:SDL2_ttf::SDL2_ttf>,SDL2_ttf::SDL2_ttf,SDL2_ttf::SDL2_ttf-static> 
                                        PRIVATE EnTT::EnTT 
                                        PRIVATE glad::glad 
                                        PRIVATE nlohmann_json nlohmann_json::nlohmann_json 
                                        PRIVATE spdlog::spdlog spdlog::spdlog_header_only 
                                        PRIVATE glm::glm  
                                        PRIVATE assimp::assimp
                                        PRIVATE ${BULLET_LIBRARIES}  
                                        PRIVATE Freetype::Freetype 
                                        PRIVATE OpenAL::OpenAL 
                                        PRIVATE EASTL  
                                        PRIVATE imgui::imgui
)


set_target_properties(3DSnake PROPERTIES 
        ARCHIVE_OUTPUT_DIRECTORY "${RELEASE_PATH}/lib"
        ARCHIVE_OUTPUT_DIRECTORY_DEBUG "${DEBUG_PATH}/lib"
        ARCHIVE_OUTPUT_DIRECTORY_RELEASE "${RELEASE_PATH}/lib"
        LIBRARY_OUTPUT_DIRECTORY "${RELEASE_PATH}/lib" 
        LIBRARY_OUTPUT_DIRECTORY_DEBUG "${DEBUG_PATH}/lib" 
        LIBRARY_OUTPUT_DIRECTORY_RELEASE "${RELEASE_PATH}/lib" 
        RUNTIME_OUTPUT_DIRECTORY "${RELEASE_PATH}" 
        RUNTIME_OUTPUT_DIRECTORY_DEBUG "${DEBUG_PATH}" 
        RUNTIME_OUTPUT_DIRECTORY_RELEASE "${RELEASE_PATH}" 

)
