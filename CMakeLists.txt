# $Id: CMakeLists.txt 1320 2014-10-26 08:12:52Z justin $

if(LFL_MOBILE)
  return()
endif()

lfl_add_target(FusionServer EXECUTABLE SOURCES fs.cpp
               LINK_LIBRARIES recognition ${LFL_APP_LIB} app_null_framework app_null_graphics
               app_null_toolkit app_null_audio app_null_camera app_opencv_matrix app_ffmpeg_fft
               app_simple_resampler app_simple_loader app_iconv_convert
               app_null_png app_null_jpeg app_null_gif app_null_ogg app_null_css app_null_ttf
               app_null_ssl app_null_js app_null_tu app_null_crashreporting ${LFL_APP_OS}
               ASSET_FILES ${LFL_APP_ASSET_FILES} ${CMAKE_CURRENT_SOURCE_DIR}/assets/*
               LIB_FILES ${LFL_APP_LIB_FILES} ${OPENCV_LIB_FILES})
lfl_post_build_start(FusionServer)

lfl_set_os_toolkit(FV)
lfl_project(FusionViewer)
lfl_add_package(FusionViewer SOURCES fv.cpp
                COMPILE_DEFINITIONS -DLFL_OPENCV INCLUDE_DIRECTORIES ${OPENCV_INCLUDE}
                LINK_LIBRARIES recognition ${LFL_APP_LIB} ${FV_FRAMEWORK} ${FV_GRAPHICS}
                ${LFL_APP_AUDIO} ${LFL_APP_CAMERA} app_opencv_matrix app_ffmpeg_fft
                app_ffmpeg_resampler app_ffmpeg_loader app_iconv_convert
                app_libpng_png app_null_jpeg app_null_gif app_null_ogg app_null_css app_null_ttf
                app_null_ssl app_null_tu app_null_js app_null_crashreporting
                app_ffmpeg_stream ${FV_TOOLKIT} ${LFL_APP_OS}
                ASSET_FILES ${LFL_APP_ASSET_FILES} ${CMAKE_CURRENT_SOURCE_DIR}/assets/*
                ${LFL_SOURCE_DIR}/core/app/assets/Nobile.*
                LIB_FILES ${LFL_APP_LIB_FILES} ${OPENCV_LIB_FILES} ${PORTAUDIO_LIB_FILES} ${FFMPEG_LIB_FILES})
lfl_post_build_start(FusionViewer)
