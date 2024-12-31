cmake_minimum_required(VERSION 3.14)

project(create-fself)
include(ExternalProject)

if (WIN32)
    set(TOOL_NAME create-fself.exe)
    set(MODFILE go-linux.mod)
else()
    set(TOOL_NAME create-fself)
    set(MODFILE go.mod)
endif()

ExternalProject_Add(create-gp4
    LOG_CONFIGURE YES
    LOG_BUILD YES
    LOG_INSTALL YES
    LOG_OUTPUT_ON_FAILURE YES
    SOURCE_DIR ${CMAKE_CURRENT_SOURCE_DIR}/cmd/create-gp4
    CONFIGURE_COMMAND ""
    BUILD_COMMAND go build -o ${TOOL_NAME} -modfile=${MODFILE}
    BUILD_IN_SOURCE 1
    INSTALL_COMMAND ""
)
set(CREATE_FSELF_BINARY ${CMAKE_CURRENT_SOURCE_DIR}/cmd/create-fself/${TOOL_NAME})
