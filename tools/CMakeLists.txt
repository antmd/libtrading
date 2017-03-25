
find_package(LibEvent REQUIRED)
find_package(ZLIB REQUIRED)
find_package(GLIB REQUIRED)
find_package(LibXml2 REQUIRED)
find_package(LibXml2 REQUIRED)
set(CURSES_NEED_NCURSES YES)
find_package(Curses REQUIRED)

set(TOOLS_INCLUDE_DIR ${CMAKE_CURRENT_SOURCE_DIR}/include)


#================================================================================
# Executable forts
#================================================================================
add_executable(forts 
	fix/fix_common.c
	cert/micex/forts.c
)
target_include_directories(forts PUBLIC
	${INCLUDE_FILES_DIR}
	${TOOLS_INCLUDE_DIR}
)
target_link_libraries(forts PUBLIC
	libtrading
	${LIBEVENT_LIB}
	${ZLIB_LIBRARIES}
	${GLIB_LIBRARIES}
	${LIBXML2_LIBRARIES}
)


#================================================================================
# Executable fast_client
#================================================================================
add_executable(fast_client
	fast/fast_client.c
	fast/test.c
)
target_include_directories(fast_client PUBLIC
	${INCLUDE_FILES_DIR}
	${TOOLS_INCLUDE_DIR}
)
target_link_libraries(fast_client PUBLIC
	libtrading
	${LIBXML2_LIBRARIES}
	${GLIB_LIBRARIES}
	${ZLIB_LIBRARIES}
	)


#================================================================================
# Executable fast_orderbook
#================================================================================
add_executable(fast_orderbook
  fast/fast_orderbook.c
)
target_include_directories(fast_orderbook PUBLIC
	${INCLUDE_FILES_DIR}
)
target_link_libraries(fast_orderbook PUBLIC
	libtrading
	${LIBEVENT_LIB}
	${ZLIB_LIBRARIES}
	${LIBXML2_LIBRARIES}
	${GLIB_LIBRARIES}
	${CURSES_LIBRARY}
)


#================================================================================
# Executable fast_parser
#================================================================================
add_executable(fast_parser
  fast/fast_parser.c
  fast/test.c
)
target_include_directories(fast_parser PUBLIC
	${INCLUDE_FILES_DIR}
	${GLIB_INCLUDE_DIRS}
)
target_link_libraries(fast_parser PUBLIC
	libtrading
	${LIBXML2_LIBRARIES}
	${GLIB_LIBRARIES}
	${ZLIB_LIBRARIES}
	)


#================================================================================
# Executable fast_server
#================================================================================
add_executable(fast_server
  fast/fast_server.c
  fast/test.c
)
target_include_directories(fast_server PUBLIC
	${INCLUDE_FILES_DIR}
	${GLIB_INCLUDE_DIRS}
)
target_link_libraries(fast_server PUBLIC
	libtrading
	${LIBXML2_LIBRARIES}
	${GLIB_LIBRARIES}
	${ZLIB_LIBRARIES}
	)


#================================================================================
# Executable fix_client
#================================================================================
add_executable(fix_client
  fix/fix_client.c
  fix/test.c
  fix/fix_common.c
)
target_include_directories(fix_client PUBLIC
	${INCLUDE_FILES_DIR}
	${TOOLS_INCLUDE_DIR}
)
target_link_libraries(fix_client PUBLIC
	libtrading
	${LIBEVENT_LIB}
	${ZLIB_LIBRARIES}
)


#================================================================================
# Executable fix_server
#================================================================================
add_executable(fix_server
  fix/fix_server.c
  fix/fix_common.c
  fix/test.c
)
target_include_directories(fix_server PUBLIC
	${INCLUDE_FILES_DIR}
	${TOOLS_INCLUDE_DIR}
)
target_link_libraries(fix_server PUBLIC
	libtrading
	${ZLIB_LIBRARIES}
	)


#================================================================================
# Executable fix_perf
#================================================================================
add_executable(fix_perf
  fix/fix_perf.c
)
target_include_directories(fix_perf PUBLIC
	${INCLUDE_FILES_DIR}
)
target_link_libraries(fix_perf PUBLIC
	libtrading
	${LIBEVENT_LIB}
	${ZLIB_LIBRARIES}
)


#================================================================================
# Executable market
#================================================================================
add_executable(market
  sim/market.c
  sim/engine.c
  fix/fix_common.c
)
target_include_directories(market PUBLIC
	${INCLUDE_FILES_DIR}
	${TOOLS_INCLUDE_DIR}
)
target_link_libraries(market PUBLIC
	libtrading
	${LIBEVENT_LIB}
	${ZLIB_LIBRARIES}
)


#================================================================================
# Executable trader
#================================================================================
add_executable(trader
	fix/fix_common.c
  sim/trader.c
)
target_include_directories(trader PUBLIC
	${INCLUDE_FILES_DIR}
	${TOOLS_INCLUDE_DIR}
)
target_link_libraries(trader PUBLIC
	libtrading
	${LIBEVENT_LIB}
	${ZLIB_LIBRARIES}
)


#================================================================================
# Executable tape
#================================================================================
add_executable(tape
  tape/tape.c
  tape/builtin-check.c
)
target_include_directories(tape PUBLIC
	${INCLUDE_FILES_DIR}
)
target_link_libraries(tape PUBLIC
	libtrading
	${LIBEVENT_LIB}
	${ZLIB_LIBRARIES}
)

