set(DRM_SOURCES
    drm_backend.cpp
    drm_output.cpp
    drm_buffer.cpp
    drm_inputeventfilter.cpp
    logging.cpp
    scene_qpainter_drm_backend.cpp
    screens_drm.cpp
)

if(HAVE_GBM)
    set(DRM_SOURCES ${DRM_SOURCES} egl_gbm_backend.cpp)
endif()

add_library(KWinWaylandDrmBackend MODULE ${DRM_SOURCES})
target_link_libraries(KWinWaylandDrmBackend kwin Libdrm::Libdrm)

if(HAVE_GBM)
    target_link_libraries(KWinWaylandDrmBackend gbm::gbm)
endif()

install(
    TARGETS
        KWinWaylandDrmBackend
    DESTINATION
        ${PLUGIN_INSTALL_DIR}/org.kde.kwin.waylandbackends/
)