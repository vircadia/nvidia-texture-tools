PROJECT(bc6h)

SET(BC6H_SRCS
	bits.h
	shapes_two.h
	tile.h
	zoh_utils.cpp
	zoh_utils.h
	zoh.cpp
	zoh.h
	zohone.cpp
	zohtwo.cpp)

ADD_LIBRARY(bc6h OBJECT ${BC6H_SRCS})
TARGET_LINK_LIBRARIES(bc6h nvcore nvmath)
TARGET_INCLUDE_DIRECTORIES(bc6h PUBLIC ${CMAKE_CURRENT_SOURCE_DIR})
