
set(LIB_INCLUDE_FILES_DIR ${INCLUDE_FILES_DIR}/libtrading)

set(DIALECTS
    micex_fix
    iex_fix
    kcg_hotspot_fix
    mbt_fix
    cme_globex_fix
    ice_os_fix
)

set(INCLUDE_FILES
    ${LIB_INCLUDE_FILES_DIR}/array.h
    ${LIB_INCLUDE_FILES_DIR}/buffer.h
    ${LIB_INCLUDE_FILES_DIR}/byte-order.h
    ${LIB_INCLUDE_FILES_DIR}/compat.h
    ${LIB_INCLUDE_FILES_DIR}/config.h
    ${LIB_INCLUDE_FILES_DIR}/die.h
    ${LIB_INCLUDE_FILES_DIR}/itoa.h
    ${LIB_INCLUDE_FILES_DIR}/order_book.h
    ${LIB_INCLUDE_FILES_DIR}/proto/bats_pitch_message.h
    ${LIB_INCLUDE_FILES_DIR}/proto/boe_message.h
    ${LIB_INCLUDE_FILES_DIR}/proto/cme_globex_fix.h
    ${LIB_INCLUDE_FILES_DIR}/proto/fast_book.h
    ${LIB_INCLUDE_FILES_DIR}/proto/fast_feed.h
    ${LIB_INCLUDE_FILES_DIR}/proto/fast_message.h
    ${LIB_INCLUDE_FILES_DIR}/proto/fast_session.h
    ${LIB_INCLUDE_FILES_DIR}/proto/fix_message.h
    ${LIB_INCLUDE_FILES_DIR}/proto/fix_session.h
    ${LIB_INCLUDE_FILES_DIR}/proto/fix_template.h
    ${LIB_INCLUDE_FILES_DIR}/proto/ice_os_fix.h
    ${LIB_INCLUDE_FILES_DIR}/proto/iex_fix.h
    ${LIB_INCLUDE_FILES_DIR}/proto/kcg_hotspot_fix.h
    ${LIB_INCLUDE_FILES_DIR}/proto/lse_itch_message.h
    ${LIB_INCLUDE_FILES_DIR}/proto/mbt_fix.h
    ${LIB_INCLUDE_FILES_DIR}/proto/mbt_quote_message.h
    ${LIB_INCLUDE_FILES_DIR}/proto/micex_fix.h
    ${LIB_INCLUDE_FILES_DIR}/proto/nasdaq_itch40_message.h
    ${LIB_INCLUDE_FILES_DIR}/proto/nasdaq_itch41_message.h
    ${LIB_INCLUDE_FILES_DIR}/proto/nyse_taq_message.h
    ${LIB_INCLUDE_FILES_DIR}/proto/omx_itch186_message.h
    ${LIB_INCLUDE_FILES_DIR}/proto/omx_moldudp_message.h
    ${LIB_INCLUDE_FILES_DIR}/proto/ouch42_message.h
    ${LIB_INCLUDE_FILES_DIR}/proto/soupbin3_session.h
    ${LIB_INCLUDE_FILES_DIR}/proto/xdp_message.h
    ${LIB_INCLUDE_FILES_DIR}/read-write.h
    ${LIB_INCLUDE_FILES_DIR}/time.h
    ${LIB_INCLUDE_FILES_DIR}/trace.h
    ${LIB_INCLUDE_FILES_DIR}/types.h
    )

set(SRC_FILES
    buffer.c
    die.c
    itoa.c
    mmap-buffer.c
    order_book.c
    read-write.c
    proto/fix_message.c
    proto/fix_session.c
    proto/fix_template.c
    proto/fast_book.c
    proto/fast_feed.c
    proto/fast_message.c
    proto/fast_session.c
    proto/fast_template.c
    proto/cme_globex_fix.c
    proto/ice_os_fix.c
    proto/micex_fix.c
    proto/iex_fix.c
    proto/kcg_hotspot_fix.c
    proto/mbt_fix.c
    proto/mbt_quote_message.c
    proto/nasdaq_itch40_message.c
    proto/nasdaq_itch41_message.c
    proto/nyse_taq_message.c
    proto/omx_itch186_message.c
    proto/ouch42_message.c
    proto/soupbin3_session.c
    proto/xdp_message.c
    proto/lse_itch_message.c
    stringencoders/modp_numtoa.c
    compat/clock_gettime.c
    )

find_package(PythonInterp REQUIRED)

foreach(DIALECT ${DIALECTS})
    add_custom_command(
        OUTPUT "${CMAKE_CURRENT_SOURCE_DIR}/proto/${DIALECT}.c"
            COMMAND ${PYTHON_EXECUTABLE} ../tools/fix/fixdialectc 
                --input "proto/${DIALECT}.dialect"
                --header-path ${LIB_INCLUDE_FILES_DIR}/proto 
                --source-path ${CMAKE_CURRENT_SOURCE_DIR}/proto
            WORKING_DIRECTORY "${CMAKE_CURRENT_SOURCE_DIR}"

        )
endforeach()

find_package(GLIB REQUIRED)
find_package(LibXml2 REQUIRED)

add_library(libtrading ${SRC_FILES} ${INCLUDE_FILES})
set_target_properties(libtrading PROPERTIES PREFIX "")

target_include_directories(libtrading PUBLIC 
    ${INCLUDE_FILES_DIR}
    ${CMAKE_CURRENT_SOURCE_DIR}/stringencoders
    ${GLIB_INCLUDE_DIRS}
    ${LIBXML2_INCLUDE_DIR}
    )
