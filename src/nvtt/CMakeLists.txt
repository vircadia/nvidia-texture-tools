PROJECT(nvtt)

ADD_SUBDIRECTORY(squish)


SET(NVTT_SRCS
    nvtt.h nvtt.cpp
    nvtt_wrapper.h nvtt_wrapper.cpp
    ClusterFit.h ClusterFit.cpp
    Compressor.h
    BlockCompressor.h BlockCompressor.cpp
    CompressorDX9.h CompressorDX9.cpp
    CompressorDX10.h CompressorDX10.cpp
    CompressorDX11.h CompressorDX11.cpp
    CompressorDXT1.h CompressorDXT1.cpp
    CompressorDXT5_RGBM.h CompressorDXT5_RGBM.cpp
    CompressorETC.h CompressorETC.cpp
    CompressorRGB.h CompressorRGB.cpp
    Context.h Context.cpp
    QuickCompressDXT.h QuickCompressDXT.cpp
    OptimalCompressDXT.h OptimalCompressDXT.cpp
    SingleColorLookup.h SingleColorLookup.cpp
    CompressionOptions.h CompressionOptions.cpp
    InputOptions.h InputOptions.cpp
    OutputOptions.h OutputOptions.cpp
    TaskDispatcher.h #TaskDispatcher.cpp
    Surface.h Surface.cpp
    CubeSurface.h CubeSurface.cpp
    cuda/CudaUtils.h cuda/CudaUtils.cpp
    cuda/CudaMath.h
    cuda/BitmapTable.h
    cuda/CudaCompressorDXT.h cuda/CudaCompressorDXT.cpp)

IF (CUDA_FOUND)
    ADD_DEFINITIONS(-DHAVE_CUDA)
    CUDA_COMPILE(CUDA_SRCS cuda/CompressKernel.cu)
    SET(NVTT_SRCS ${NVTT_SRCS} ${CUDA_SRCS})
    SET(LIBS ${LIBS} ${CUDA_LIBRARIES})
    INCLUDE_DIRECTORIES(${CUDA_INCLUDE_DIRS})
ENDIF (CUDA_FOUND)

INCLUDE_DIRECTORIES(${CMAKE_CURRENT_SOURCE_DIR})
INCLUDE_DIRECTORIES(${NV_SOURCE_DIR}/extern/rg_etc1_v104)

if (BUILD_SHARED_LIBS)
    ADD_DEFINITIONS(-DNVTT_EXPORTS)
    ADD_DEFINITIONS(-DNVTT_SHARED=1)
endif()

ADD_LIBRARY(nvtt 
    ${NVTT_SRCS} 
    $<TARGET_OBJECTS:nvcore>
    $<TARGET_OBJECTS:nvimage>
    $<TARGET_OBJECTS:nvthread>
    $<TARGET_OBJECTS:bc6h>
    $<TARGET_OBJECTS:bc7>
    $<TARGET_OBJECTS:nvmath>
)

target_link_libraries(nvtt squish rg_etc1)

IF(PNG_FOUND)
    SET(LIBS ${LIBS} ${PNG_LIBRARIES})
    TARGET_INCLUDE_DIRECTORIES(nvtt PRIVATE ${PNG_INCLUDE_DIR})
ENDIF(PNG_FOUND)

IF(JPEG_FOUND)
    SET(LIBS ${LIBS} ${JPEG_LIBRARIES})
    TARGET_INCLUDE_DIRECTORIES(nvtt PRIVATE ${JPEG_INCLUDE_DIR})
ENDIF(JPEG_FOUND)

IF(TIFF_FOUND)
    SET(LIBS ${LIBS} ${TIFF_LIBRARIES})
    TARGET_INCLUDE_DIRECTORIES(nvtt PRIVATE ${TIFF_INCLUDE_DIR})
ENDIF(TIFF_FOUND)

IF(OPENEXR_FOUND)
    SET(LIBS ${LIBS} ${OPENEXR_LIBRARIES})
    TARGET_INCLUDE_DIRECTORIES(nvtt PRIVATE ${OPENEXR_INCLUDE_PATHS})
ENDIF(OPENEXR_FOUND)

IF(FREEIMAGE_FOUND)
    SET(LIBS ${LIBS} ${FREEIMAGE_LIBRARIES})
    TARGET_INCLUDE_DIRECTORIES(nvtt PRIVATE ${FREEIMAGE_INCLUDE_PATH})
ENDIF(FREEIMAGE_FOUND)

if (LIBS)
    TARGET_LINK_LIBRARIES(nvtt ${LIBS})
endif()

INSTALL(TARGETS nvtt 
    RUNTIME DESTINATION bin
    LIBRARY DESTINATION lib
    ARCHIVE DESTINATION lib)
INSTALL(FILES nvtt.h nvtt_wrapper.h DESTINATION include/nvtt)

if(BUILD_TOOLS)
    ADD_SUBDIRECTORY(tools)
endif()

if(BUILD_TESTS)
    ADD_SUBDIRECTORY(tests)
endif()
