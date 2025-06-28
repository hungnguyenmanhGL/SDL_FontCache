cmake_minimum_required(VERSION 3.1)
project(SDL_FontCache VERSION 0.10.0 LANGUAGES C)

find_package(SDL2 REQUIRED)
find_package(SDL2_ttf REQUIRED)

add_library(FontCache
    SDL_FontCache.h
    SDL_FontCache.c
)
target_include_directories(FontCache PUBLIC .) # Keep this for its own headers
target_link_libraries(FontCache PUBLIC SDL2::SDL2 SDL2_ttf::SDL2_ttf) # Link directly to imported targets

add_executable(FontCache-tests
	test/main.c
)
file(COPY test/utf8_sample.txt DESTINATION ${CMAKE_BINARY_DIR})
file(COPY test/fonts/FreeSans.ttf DESTINATION ${CMAKE_BINARY_DIR}/fonts)
target_link_libraries(FontCache-tests FontCache m)


