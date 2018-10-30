PROJECT(nvmath)

SET(MATH_SRCS
    nvmath.h
    Box.h Box.inl
    Color.h Color.inl
    Fitting.h Fitting.cpp
    Gamma.h Gamma.cpp
    Half.h Half.cpp
    Matrix.h Matrix.inl Matrix.cpp
    Plane.h Plane.inl Plane.cpp
    SphericalHarmonic.h SphericalHarmonic.cpp
    SimdVector.h SimdVector_SSE.h SimdVector_VE.h
    Vector.h Vector.inl)



# targets
ADD_LIBRARY(nvmath OBJECT ${MATH_SRCS})
TARGET_INCLUDE_DIRECTORIES(nvmath PUBLIC ${CMAKE_CURRENT_SOURCE_DIR})