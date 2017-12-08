#
# apps/CMakeLists.txt
#

add_executable(sipauthserve
	sipauthserve.cpp
	../servershare.cpp
	../NodeManager/JSONDB/JSONDB.cpp
)

target_link_libraries(sipauthserve
	openbts-sr
	openbts-sr-globals
	openbts-common
	openbts-nodemanager
	${OPENBTS_COMMON_LIBRARIES}
	zmq
	ortp
	osipparser2
	osip2
)

add_executable(comp128 comp128.c)
target_link_libraries(comp128
	openbts-sr-globals
	openbts-common
	openbts-nodemanager
)

install(TARGETS comp128 sipauthserve
	RUNTIME DESTINATION bin
	LIBRARY DESTINATION lib
	ARCHIVE DESTINATION lib
)
