cmake_minimum_required(VERSION 3.16)
project(AAAAA C)

set(CMAKE_TOOLCHAIN_FILE libs/cget/cget/cget.cmake)

set(CMAKE_C_STANDARD 11)
#Compilation Options for now for Test reasons
option(USE_TESTS "Compile and proof the game by unit testing" ON)

#We configure the compilers


#Set Variables for later
set(SOURCE_FILES src/main.c
        )

#We now crossplatform af (This is bad practice, setup FIND_LIBRARY later buuuuut I AM LAZY)
file(GLOB LINK_SUBDIRS LIST_DIRECTORIES true RELATIVE ${PROJECT_SOURCE_DIR} libs/cget/lib/*/)
#For real opengl and vulkan now
find_package(OpenGL REQUIRED)
find_package(Vulkan REQUIRED)
link_directories(libs/cget/lib/ ${LINK_SUBDIRS})


set(INCLUDE_DIRECTORIES
        ${PROJECT_SOURCE_DIR}/include
        ${PROJECT_SOURCE_DIR}/libs/cget/include/
        ${PROJECT_SOURCE_DIR}/libs/cget/lib/mimalloc-1.6/include
        ${OPENGL_INCLUDE_DIR}
        ${Vulkan_INCLUDE_DIRS})
include_directories(${PROJECT_SOURCE_DIR}/libs/cget/include/)



#We add the executable
add_executable(AAAAA ${SOURCE_FILES})
#We add the include headers
target_include_directories(AAAAA PRIVATE ${INCLUDE_DIRECTORIES})
#Finally we link all the stuff
target_link_libraries(AAAAA
        glfw3
        bgfx
        bimg
        bx
        flecs
        log
        chipmunk
        mimalloc
        ${OPENGL_LIBRARIES}
        ${Vulkan_LIBRARIES})


######################################
############EXTRA ROUND###############
##############TESTING#################
######################################
if(USE_TEST)
    enable_testing()
    set(TESTABLE_CODE )
    set(TESTABLE_INCLUDE )
    add_library(AAAAA_TESTEABLE ${TESTABLE_CODE})
    target_include_directories(AAAAA_TESTABLE PUBLIC ${TESTABLE_INCLUDE})
    target_link_libraries()
    set(UNIT_TEST_SOURCE_FILES )
    add_executable(AAAAA_TESTS ${UNIT_TEST_SOURCE_FILES})

    target_link_libraries(AAAAA_TESTS
            AAAAA_TESTEABLE
            glfw3
            bgfx
            bimg
            bx
            flecs
            log
            chipmunk
            mimalloc
            cmocka
            ${OPENGL_LIBRARIES}
            ${Vulkan_LIBRARIES})
    add_test(TEST_ALL AAAAA_TESTS)



endif()

