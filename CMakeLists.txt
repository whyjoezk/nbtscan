cmake_minimum_required(VERSION 3.17)
project(nbtscan C)

set(CMAKE_C_STANDARD 11)

file(GLOB SOURCES
        all_digitsA.c
        byteswap_nodestats.c
        die.c
        display_nbtstat.c
        dump_packet.c
        errors.c
        gen_perl.c
        hostname.c
        lookup_hostname.c
        nbtdefs.h
        nbtscan.c
        libcommon.h
        netbios_fixname.c
        netbios_name.c
        netbios_pack.c
        netbios_unpack.c
        netmasks.c
        nstrcpyA.c
        packetio.c
        parse_inaddr.c
        parse_nbtstat.c
        parse_target.c
        parse_target_cb.c
        penlib.h
        printable_NETBIOS_question_class.c
        printable_NETBIOS_question_type.c
        process_response.c
        sleep_msecs.c                                                                                                           stripA.c                                                                                                                targets.c                                                                                                               timeval_set_secs.c                                                                                                      version.c                                                                                                               winsock.c                                                                                                               win_sock.h
        )

if(WIN32)
	link_libraries(wsock32)
endif()
if ("${CMAKE_C_COMPILER_ID}" STREQUAL "Clang")
    set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS}")
else()
     set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} -s")
endif()
add_executable(nbtscan nbtscan.c ${SOURCE_FILES} ${SOURCES})
if(ANDROID)
    if (CMAKE_CXX_COMPILER_ID MATCHES Clang AND CMAKE_BUILD_TYPE STREQUAL Release)
        add_custom_command(TARGET ${PROJECT_NAME} POST_BUILD COMMAND ${CMAKE_STRIP} ${CMAKE_PROJECT_NAME} COMMENT "Strip debug symbols done on final binary.")
    endif()
endif()
