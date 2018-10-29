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
TARGET_LINK_LIBRARIES(nvimage ${LIBS} nvcore posh bc6h bc7 nvmath)
TARGET_INCLUDE_DIRECTORIES(nvimage PUBLIC ${CMAKE_CURRENT_SOURCE_DIR})

IF(PNG_FOUND)
    SET(LIBS ${LIBS} ${PNG_LIBRARIES})
    TARGET_INCLUDE_DIRECTORIES(nvimage PRIVATE ${PNG_INCLUDE_DIR})
ENDIF(PNG_FOUND)

IF(JPEG_FOUND)
    SET(LIBS ${LIBS} ${JPEG_LIBRARIES})
    TARGET_INCLUDE_DIRECTORIES(nvimage PRIVATE ${JPEG_INCLUDE_DIR})
ENDIF(JPEG_FOUND)

IF(TIFF_FOUND)
    SET(LIBS ${LIBS} ${TIFF_LIBRARIES})
    TARGET_INCLUDE_DIRECTORIES(nvimage PRIVATE ${TIFF_INCLUDE_DIR})
ENDIF(TIFF_FOUND)

IF(OPENEXR_FOUND)
    SET(LIBS ${LIBS} ${OPENEXR_LIBRARIES})
    TARGET_INCLUDE_DIRECTORIES(nvimage PRIVATE ${OPENEXR_INCLUDE_PATHS})
ENDIF(OPENEXR_FOUND)

IF(FREEIMAGE_FOUND)
    SET(LIBS ${LIBS} ${FREEIMAGE_LIBRARIES})
    TARGET_INCLUDE_DIRECTORIES(nvimage PRIVATE ${FREEIMAGE_INCLUDE_PATH})
ENDIF(FREEIMAGE_FOUND)

if (LIBS)
    TARGET_LINK_LIBRARIES(nvimage ${LIBS})
endif()
