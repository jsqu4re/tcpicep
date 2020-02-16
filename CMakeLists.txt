cmake_minimum_required(VERSION 3.5)
project(tcpicep)

include(GNUInstallDirs)

find_package(iceoryx_posh CONFIG REQUIRED)

add_executable(tcpicep-gateway ./source/tcpicep-gateway.cpp)
target_link_libraries(tcpicep-gateway
    iceoryx_posh::iceoryx_posh
)

install(
    TARGETS tcpicep-gateway
    RUNTIME DESTINATION bin
)
