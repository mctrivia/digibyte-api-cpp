FIND_PACKAGE(JSONCPP REQUIRED)
FIND_PACKAGE(JSONRPCCPP REQUIRED)
FIND_PACKAGE(CURL REQUIRED)

# Find header and source files
FILE(GLOB digibyteapi_header ${CMAKE_CURRENT_SOURCE_DIR}/*.h)
FILE(GLOB digibyteapi_source ${CMAKE_CURRENT_SOURCE_DIR}/*.cpp)

# Set target libraries
ADD_LIBRARY(digibyteapi SHARED ${digibyteapi_source})
ADD_LIBRARY(digibyteapi_static STATIC ${digibyteapi_source})

# Set output name of static library
SET_TARGET_PROPERTIES(digibyteapi_static PROPERTIES OUTPUT_NAME digibyteapi)

# Link the library with json-rpc-cpp libs
TARGET_LINK_LIBRARIES(digibyteapi
                        ${CURL_LIBRARY}
                        ${JSONCPP_LIBRARY}
                        jsonrpccpp-common
                        jsonrpccpp-client)

TARGET_LINK_LIBRARIES(digibyteapi_static
                        ${CURL_LIBRARY}
                        ${JSONCPP_LIBRARY}
                        jsonrpccpp-common
                        jsonrpccpp-client)

# Set version settings
SET(VERSION_STRING ${MAJOR_VERSION}.${MINOR_VERSION}.${PATCH_VERSION})
SET_TARGET_PROPERTIES(digibyteapi digibyteapi_static PROPERTIES
    VERSION "${VERSION_STRING}"
    SOVERSION "${SO_VERSION}")

# Install to appropriate destinations
INSTALL(FILES ${digibyteapi_header} DESTINATION include/digibyteapi)

INSTALL(TARGETS digibyteapi digibyteapi_static
            LIBRARY DESTINATION lib
            ARCHIVE DESTINATION lib)
