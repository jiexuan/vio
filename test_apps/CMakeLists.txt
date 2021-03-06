set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -lprofiler")

include_directories(
  ${CMAKE_CURRENT_SOURCE_DIR}/include
)

file(GLOB SOURCE_FILE
    "include/*.hpp"
    "src/*.cpp"
)

message(STATUS "${SOURCE_FILE}")

set(TARGET "vio_app")

add_library(${TARGET} SHARED ${SOURCE_FILE})
target_link_libraries( ${TARGET} 
                       util
                       multiview_helper
                       mapdata
                       feature_tracker
                       graph_optimizer
                       pnp_estimator
                       map_initializer
                       ${OpenCV_LIBS} )

add_executable( vio_app_test test/vio_app.cpp)
target_link_libraries( vio_app_test
                       ${TARGET}
                       ${OpenCV_LIBS} )
