cmake_minimum_required( VERSION 3.6.0 )

#
# Common
#
project ( msdfgen )

add_library( msdfgen STATIC "" )
target_compile_options( msdfgen PRIVATE -Wall )

target_sources ( msdfgen
    PRIVATE
    ext/import-font.cpp
    ext/import-svg.cpp
    ext/save-png.cpp
    lib/lodepng.cpp
    lib/tinyxml2.cpp
    msdfCore/Bitmap.cpp
    msdfCore/Contour.cpp
    msdfCore/edge-coloring.cpp
    msdfCore/EdgeHolder.cpp
    msdfCore/edge-segments.cpp
    msdfCore/equation-solver.cpp
    msdfCore/msdfgen.cpp
    msdfCore/render-sdf.cpp
    msdfCore/save-bmp.cpp
    msdfCore/Shape.cpp
    msdfCore/shape-description.cpp
    msdfCore/SignedDistance.cpp
    msdfCore/Vector2.cpp 
)

target_include_directories( msdfgen PRIVATE 
	./ext
	./include
	./include/freetype
	./msdfCore
)

target_compile_definitions( msdfgen PRIVATE NOMINMAX )
target_compile_features( msdfgen PRIVATE cxx_std_11 )

target_link_libraries( msdfgen PUBLIC 
	C:/Users/hudeming/Desktop/TianFuKang/msdfgen/MSDF/lib/freetype.lib
)
