cmake_minimum_required(VERSION 3.16...3.25)

find_package(FFmpeg REQUIRED COMPONENTS avcodec avdevice avutil avformat)

add_library(media-playback INTERFACE EXCLUDE_FROM_ALL)
add_library(OBS::media-playback ALIAS media-playback)

target_sources(
  media-playback
  INTERFACE media-playback/media.c
            media-playback/media.h
            media-playback/cache.c
            media-playback/cache.h
            media-playback/decode.c
            media-playback/decode.h
            media-playback/media-playback.c
            media-playback/media-playback.h
            media-playback/closest-format.h)

target_include_directories(media-playback INTERFACE "${CMAKE_CURRENT_SOURCE_DIR}")
target_compile_options(media-playback INTERFACE ${ARCH_SIMD_FLAGS})
target_compile_definitions(media-playback INTERFACE ${ARCH_SIMD_DEFINES})

target_link_libraries(media-playback INTERFACE FFmpeg::avcodec FFmpeg::avdevice FFmpeg::avutil FFmpeg::avformat)
