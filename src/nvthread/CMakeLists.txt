PROJECT(nvthread)

SET(THREAD_SRCS
	nvthread.h nvthread.cpp
	Atomic.h
	Event.h Event.cpp
	Mutex.h Mutex.cpp
	ParallelFor.h ParallelFor.cpp
	Thread.h Thread.cpp
	ThreadPool.h ThreadPool.cpp)

ADD_LIBRARY(nvthread OBJECT ${THREAD_SRCS})
TARGET_INCLUDE_DIRECTORIES(nvthread PUBLIC ${CMAKE_CURRENT_SOURCE_DIR})
