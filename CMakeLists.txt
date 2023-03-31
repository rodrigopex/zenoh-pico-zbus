cmake_minimum_required(VERSION 3.22.1)

if (BOARD MATCHES "rpi_pico")
    add_definitions(-DZENOH_NO_STDATOMIC)
endif ()

find_package(Zephyr REQUIRED HINTS $ENV{ZEPHYR_BASE})
project(zenoh_pico_zbus)

set(ZENOHPICO_INCLUDE_DIR ${CMAKE_SOURCE_DIR}/zenoh-pico/include)

file(GLOB Sources
        "zenoh-pico/src/*.c"
        "zenoh-pico/src/api/*.c"
        "zenoh-pico/src/net/*.c"
        "zenoh-pico/src/collections/*.c"
        "zenoh-pico/src/link/*.c"
        "zenoh-pico/src/link/config/*.c"
        "zenoh-pico/src/link/unicast/*.c"
        #        "zenoh-pico/src/link/multicast/*.c"
        "zenoh-pico/src/protocol/*.c"
        "zenoh-pico/src/protocol/keyexpr/*.c"
        "zenoh-pico/src/session/*.c"
        "zenoh-pico/src/system/zephyr/*.c"
        "zenoh-pico/src/transport/*.c"
        "zenoh-pico/src/transport/common/*.c"
        "zenoh-pico/src/transport/unicast/*.c"
        "zenoh-pico/src/transport/unicast/link/*.c"
        "zenoh-pico/src/transport/unicast/link/task/*.c"
        #        "zenoh-pico/src/transport/multicast/*.c"
        #        "zenoh-pico/src/transport/multicast/link/*.c"
        #        "zenoh-pico/src/transport/multicast/link/task/*.c"
        "zenoh-pico/src/utils/*.c"
        )

add_definitions(-DZENOH_ZEPHYR)

include_directories(app PUBLIC ${ZENOHPICO_INCLUDE_DIR})
#target_link_libraries(app PUBLIC zenohpico_lib)

target_sources(app
        PRIVATE
        ${Sources}
        src/main.c
        )
