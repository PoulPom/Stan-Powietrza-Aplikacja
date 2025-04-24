cmake_minimum_required(VERSION 3.21)
project(AirQualityApp)

set(CMAKE_CXX_STANDARD 17)

# Ustaw toolchain vcpkg
set(CMAKE_TOOLCHAIN_FILE "C:/vcpkg/scripts/buildsystems/vcpkg.cmake"
    CACHE STRING "Vcpkg toolchain file")

# Znajdź Boost z wymaganymi komponentami
find_package(Boost REQUIRED COMPONENTS asio system)

# Znajdź wxWidgets
find_package(wxWidgets REQUIRED COMPONENTS core base)

# Znajdź nlohmann-json
find_package(nlohmann_json CONFIG REQUIRED)

# Dołącz wxWidgets
include(${wxWidgets_USE_FILE})

# Dodaj plik wykonywalny jako aplikację GUI
add_executable(AirQualityApp WIN32 main.cpp)

# Podlinkuj biblioteki
target_link_libraries(AirQualityApp
    PRIVATE
    Boost::asio
    Boost::system
    nlohmann_json::nlohmann_json
    ${wxWidgets_LIBRARIES}
)