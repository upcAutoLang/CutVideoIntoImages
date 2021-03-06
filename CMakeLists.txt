CMAKE_MINIMUM_REQUIRED(VERSION 2.8)
PROJECT(CutVideoIntoImages)

SET(EXECUTABLE_OUTPUT_PATH ${PROJECT_BINARY_DIR}/bin)
SET(LIBRARY_OUTPUT_PATH ${PROJECT_BINARY_DIR}/lib)

FIND_PACKAGE(OpenCV REQUIRED)
LINK_DIRECTORIES(${PROJECT_BINARY_DIR}/lib)

INCLUDE_DIRECTORIES(./)
INCLUDE_DIRECTORIES(./src)

SET(LIB_CUTVIDEOINTOIMAGE_SOURCE
	./src/CutVideoIntoImages.h
	./src/CutVideoIntoImages.cpp)
SET(LIB_QSDIRFUN_SOURCE
	./src/qsDirFun.h
	./src/qsDirFun.cpp)
SET(LIB_QSSTRINGFUN_SOURCE
	./src/qsStringFun.h
	./src/qsStringFun.cpp)

ADD_LIBRARY(cutvideointoimages SHARED ${LIB_CUTVIDEOINTOIMAGE_SOURCE})
ADD_LIBRARY(qsdirfun SHARED ${LIB_QSDIRFUN_SOURCE})
ADD_LIBRARY(qsstringfun SHARED ${LIB_QSSTRINGFUN_SOURCE})

TARGET_LINK_LIBRARIES(cutvideointoimages
	${OpenCV_LIBS})
TARGET_LINK_LIBRARIES(qsdirfun)
TARGET_LINK_LIBRARIES(qsstringfun)

SET(LIB_CUTVIDEOINTOIMAGE
	cutvideointoimages qsdirfun qsstringfun)

ADD_EXECUTABLE(CutVideoIntoImages ./src/main.cpp)
TARGET_LINK_LIBRARIES(CutVideoIntoImages
	${LIB_CUTVIDEOINTOIMAGE})
