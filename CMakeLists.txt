cmake_minimum_required( VERSION 3.6.0 )

project ( fontue )

set( PATHNAME "./core" )
set( PATHNAME_ "./MSDF" )

add_subdirectory( ${PATHNAME} vrs-core )
add_subdirectory( ${PATHNAME_} msdfgen )

add_executable( fontue 
	main.cpp 
)

target_include_directories( fontue PRIVATE 
	${PATHNAME}
	${PATHNAME}/Android 
	${PATHNAME}/Kernel 
	./MSDF 
	./MSDF/ext
	./MSDF/include
	./MSDF/include/freetype
	./MSDF/msdfCore
)

target_link_libraries( fontue PRIVATE 
	vrs-core 
	msdfgen 
)