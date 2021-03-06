cmake_minimum_required(VERSION 2.8.7 FATAL_ERROR)
project(RetinaSegmentation)

set(CMAKE_BUILD_TYPE "Debug")

set(CMAKE_CXX_FLAGS ${CMAKE_CXX_FLAGS} -std=c++11)


Find_package( CUDA )
include_directories( ${CUDA_TOOLKIT_ROOT_DIR}/include )
link_directories( ${CUDA_TOOLKIT_ROOT_DIR}/lib64 )
set( CUDA_LIBRARIES libcublas.so libcudart.so libcufft.so )
Message(${CUDA_LIBRARIES})

set( OTHER_LIBRARIES libprotobuf.so )


include_directories(HeaderFiles/Reference)
include_directories(HeaderFiles/Reference/caffe)
include_directories(HeaderFiles/Reference/opencv)
include_directories(HeaderFiles/Reference/opencv2)
include_directories(HeaderFiles/ThisProject/Preprocessing)
include_directories(HeaderFiles/ThisProject/CNNSeg)



link_directories(${CMAKE_CURRENT_SOURCE_DIR}/lib)

set( CPU_ONLY 1)
set( CAFFE_LIBRARIES libcaffe.so )
set( OPENCV_LIBRARIES libopencv_core.so libopencv_highgui.so libopencv_imgproc.so)

add_executable(RetinaSegmentation src/main.cpp )
target_link_libraries(RetinaSegmentation  ${CAFFE_LIBRARIES} ${OPENCV_LIBRARIES} ${CUDA_LIBRARIES} ${OTHER_LIBRARIES} )


