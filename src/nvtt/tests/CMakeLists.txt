
ADD_EXECUTABLE(filtertest filtertest.cpp ../tools/cmdline.h)
TARGET_LINK_LIBRARIES(filtertest nvtt)

ADD_EXECUTABLE(nvtestsuite testsuite.cpp)
TARGET_LINK_LIBRARIES(nvtestsuite nvtt)
ADD_TEST(NVTT.TestSuite.Kodak.cuda nvtestsuite -path ${NV_SOURCE_DIR}/data/testsuite -set 0 -out output-cuda-kodak)
ADD_TEST(NVTT.TestSuite.Waterloo.cuda nvtestsuite -path ${NV_SOURCE_DIR}/data/testsuite -set 1 -out output-cuda-waterloo)
ADD_TEST(NVTT.TestSuite.Epic.cuda nvtestsuite -path ${NV_SOURCE_DIR}/data/testsuite -set 2 -out output-cuda-epic)
ADD_TEST(NVTT.TestSuite.Kodak.nocuda nvtestsuite -path ${NV_SOURCE_DIR}/data/testsuite -set 0 -nocuda -out output-nocuda-kodak)
ADD_TEST(NVTT.TestSuite.Waterloo.nocuda nvtestsuite -path ${NV_SOURCE_DIR}/data/testsuite -set 1 -nocuda -out output-nocuda-waterloo)
ADD_TEST(NVTT.TestSuite.Epic.nocuda nvtestsuite -path ${NV_SOURCE_DIR}/data/testsuite -set 2 -nocuda -out output-nocuda-epic)

IF (CUDA_FOUND)
    ADD_EXECUTABLE(driverapitest driverapi.cpp)
    TARGET_LINK_LIBRARIES(driverapitest nvtt)
ENDIF (CUDA_FOUND)

ADD_EXECUTABLE(imperativeapi imperativeapi.cpp)
TARGET_LINK_LIBRARIES(imperativeapi nvtt)

ADD_EXECUTABLE(process_alpha_map process_alpha_map.cpp)
TARGET_LINK_LIBRARIES(process_alpha_map nvtt)

ADD_EXECUTABLE(cubemaptest cubemaptest.cpp)
TARGET_LINK_LIBRARIES(cubemaptest nvtt)

ADD_EXECUTABLE(nvhdrtest hdrtest.cpp)
TARGET_LINK_LIBRARIES(nvhdrtest nvtt)

INSTALL(TARGETS nvtestsuite nvhdrtest DESTINATION bin)
 
#include_directories("/usr/include/ffmpeg/")
#ADD_EXECUTABLE(nvmpegenc tools/mpegenc.cpp tools/cmdline.h)
#TARGET_LINK_LIBRARIES(nvmpegenc nvcore nvmath nvimage avcodec z)
#INSTALL(TARGETS nvmpegenc DESTINATION bin)

