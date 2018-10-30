PROJECT(nvimage)

SET(IMAGE_SRCS	
    nvimage.h
    BlockDXT.h BlockDXT.cpp
    ColorBlock.h ColorBlock.cpp
    DirectDrawSurface.h DirectDrawSurface.cpp
    ErrorMetric.h ErrorMetric.cpp
    Filter.h Filter.cpp
    FloatImage.h FloatImage.cpp
    Image.h Image.cpp
    ImageIO.h ImageIO.cpp
    #KtxFile.h KtxFile.cpp
    NormalMap.h NormalMap.cpp
    PixelFormat.h
    PsdFile.h
    TgaFile.h
    KtxFile.h KtxFile.cpp)

ADD_LIBRARY(nvimage OBJECT ${IMAGE_SRCS})
TARGET_INCLUDE_DIRECTORIES(nvimage PUBLIC ${CMAKE_CURRENT_SOURCE_DIR})
