PROJECT(nvcore)

SET(CORE_SRCS
    nvcore.h
    Array.h
    Debug.h Debug.cpp
    DefsGnucDarwin.h
    DefsGnucLinux.h
    DefsGnucWin32.h
    DefsVcWin32.h
    FileSystem.h FileSystem.cpp
    ForEach.h
    Memory.h Memory.cpp
    Ptr.h
    RefCounted.h
    StrLib.h StrLib.cpp
    Stream.h
    StdStream.h
    TextWriter.h TextWriter.cpp
    Timer.h Timer.cpp
    Utils.h)

IF(UNIX)
    SET(LIBS ${LIBS} ${CMAKE_DL_LIBS})
ENDIF(UNIX)

ADD_LIBRARY(nvcore OBJECT ${CORE_SRCS})
TARGET_LINK_LIBRARIES(nvcore ${LIBS})
TARGET_INCLUDE_DIRECTORIES(nvcore PUBLIC ${CMAKE_CURRENT_SOURCE_DIR})

# On NetBSD and FreeBSD backtrace() is provided by libexecinfo, not libc.
if (CMAKE_SYSTEM_NAME MATCHES "NetBSD" OR CMAKE_SYSTEM_NAME MATCHES "FreeBSD")
     TARGET_LINK_LIBRARIES(nvcore execinfo)
endif()
