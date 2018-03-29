cmake_minimum_required(VERSION 3.1)

project(fb1-5 C)

find_package(BISON)
find_package(FLEX)

BISON_TARGET(MyParser ../${PROJECT_NAME}.y 
             ${CMAKE_CURRENT_BINARY_DIR}/${PROJECT_NAME}.tab.c)

FLEX_TARGET(MyScanner ../${PROJECT_NAME}.l  
            ${CMAKE_CURRENT_BINARY_DIR}/${PROJECT_NAME}.yy.c)

ADD_FLEX_BISON_DEPENDENCY(MyScanner MyParser)

add_executable(${PROJECT_NAME}
    ${BISON_MyParser_OUTPUTS}
    ${FLEX_MyScanner_OUTPUTS}
)

target_include_directories(${PROJECT_NAME}
    PRIVATE 
    .  
    ${CMAKE_CURRENT_BINARY_DIR}
)

target_link_libraries(${PROJECT_NAME}
    ${BISON_LIBRARIES}
    ${FLEX_LIBRARIES}
)



