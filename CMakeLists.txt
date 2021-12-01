project(codal-nimble)

include("${CODAL_UTILS_LOCATION}")

#set(CMAKE_CXX_CLANG_TIDY
#    clang-tidy;
#    --extra-arg=-std=c++17;
#    --extra-arg=-Wno-error;
#    --extra-arg=-Wno-register;)


list(APPEND INCLUDE_DIRS
    "${CMAKE_CURRENT_SOURCE_DIR}/ext/tinycrypt/include/"
    "${CMAKE_CURRENT_SOURCE_DIR}/nimble/include/"
    "${CMAKE_CURRENT_SOURCE_DIR}/nimble/controller/include/"
    "${CMAKE_CURRENT_SOURCE_DIR}/nimble/host/include/"
    "${CMAKE_CURRENT_SOURCE_DIR}/nimble/host/mesh/include/"
    # "${CMAKE_CURRENT_SOURCE_DIR}/nimble/host/src/services/..."
    # "${CMAKE_CURRENT_SOURCE_DIR}/nimble/transport/..."
    "${CMAKE_CURRENT_SOURCE_DIR}/porting/nimble/include/"
    "${CMAKE_CURRENT_SOURCE_DIR}/porting/npl/dummy/include/"
    # "${CMAKE_CURRENT_SOURCE_DIR}/porting/npl/freertos/include/"
    # "${CMAKE_CURRENT_SOURCE_DIR}/porting/npl/linux/include/"
    # "${CMAKE_CURRENT_SOURCE_DIR}/porting/npl/mynewt/include/"
    # "${CMAKE_CURRENT_SOURCE_DIR}/porting/npl/nuttx/include/"
    # "${CMAKE_CURRENT_SOURCE_DIR}/porting/npl/riot/include/"
)

list(APPEND CPP_SOURCE_FILES)

RECURSIVE_FIND_FILE(C_SOURCE_FILES "${CMAKE_CURRENT_SOURCE_DIR}/ext/" "*.c")
RECURSIVE_FIND_FILE(C_SOURCE_FILES "${CMAKE_CURRENT_SOURCE_DIR}/nimble/controller" "*.c")
RECURSIVE_FIND_FILE(C_SOURCE_FILES "${CMAKE_CURRENT_SOURCE_DIR}/nimble/host" "*.c")
RECURSIVE_FIND_FILE(C_SOURCE_FILES "${CMAKE_CURRENT_SOURCE_DIR}/porting/nimble" "*.c")
RECURSIVE_FIND_FILE(C_SOURCE_FILES "${CMAKE_CURRENT_SOURCE_DIR}/porting/npl/dummy" "*.c")
list(APPEND C_SOURCE_FILES )

# add them
include_directories(${INCLUDE_DIRS})

# create our target
add_library(codal-nimble ${C_SOURCE_FILES} ${CPP_SOURCE_FILES})

#target_link_libraries(codal-stm32 codal-core)

# expose it to parent cmake.
target_include_directories(codal-nimble PUBLIC ${INCLUDE_DIRS})
