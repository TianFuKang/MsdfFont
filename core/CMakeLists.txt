cmake_minimum_required( VERSION 3.6.0 )

#
# Common
#
project ( libvrs-core )

add_library( vrs-core STATIC "" )
target_compile_options( vrs-core PRIVATE -Wall )

target_sources ( vrs-core
    PRIVATE
    Kernel/OVR_Alg.cpp
    Kernel/OVR_Allocator.cpp
    Kernel/OVR_Atomic.cpp
    Kernel/OVR_BinaryFile.cpp
    Kernel/OVR_File.cpp
    Kernel/OVR_FileFILE.cpp
    Kernel/OVR_Geometry.cpp
    #Kernel/OVR_GlUtils.cpp
    Kernel/OVR_JSON.cpp
    Kernel/OVR_Lexer.cpp
    Kernel/OVR_Lockless.cpp
    Kernel/OVR_Log.cpp
    Kernel/OVR_LogUtils.cpp
    Kernel/OVR_MappedFile.cpp
    Kernel/OVR_Math.cpp
    Kernel/OVR_MemBuffer.cpp
    Kernel/OVR_RefCount.cpp
    Kernel/OVR_Signal.cpp
    Kernel/OVR_Std.cpp
    Kernel/OVR_String.cpp
    Kernel/OVR_String_FormatUtil.cpp
    Kernel/OVR_String_PathUtil.cpp
    Kernel/OVR_SysFile.cpp
    Kernel/OVR_System.cpp
    Kernel/OVR_ThreadCommandQueue.cpp
    Kernel/OVR_TypesafeNumber.cpp
    Kernel/OVR_UTF8Util.cpp
)

#
# Platform special
#
if ( CMAKE_SYSTEM_NAME STREQUAL Android )

    target_sources( vrs-core
                 PRIVATE
                 Kernel/OVR_ThreadsPthread.cpp
                    Android/JniUtils.cpp
                 )
    target_compile_definitions( vrs-core PUBLIC GRAPHICS_API_OPENGL_ES=1 )
    target_compile_options( vrs-core PRIVATE -Wextra -Wconversion -Wno-unused-function )
    #target_compile_features( vrs-core PUBLIC cxx_std_11 )
    find_library( log-lib log )
    target_link_libraries( vrs-core ${log-lib} )

elseif ( CMAKE_SYSTEM_NAME STREQUAL Darwin )

    target_sources( vrs-core
                     PRIVATE
                     Kernel/OVR_ThreadsPthread.cpp
                     )
    target_compile_options( vrs-core PRIVATE -Wextra -Wconversion -Wno-unused-function )
    target_compile_features( vrs-core PRIVATE cxx_std_11 )

else ( CMAKE_SYSTEM_NAME STREQUAL Windows )

    target_sources( vrs-core
                     PRIVATE
                     Kernel/OVR_ThreadsWinAPI.cpp
                     )
    target_compile_definitions( vrs-core PRIVATE NOMINMAX )
    target_compile_features( vrs-core PRIVATE cxx_std_11 )

endif ()