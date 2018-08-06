file(GLOB sources "*.cpp")
file(GLOB headers "*.h")

add_library(devcore ${sources} ${headers})

add_compile_options(-Wshorten-64-to-32)

# Needed to prevent including system-level boost headers:
target_include_directories(devcore SYSTEM PUBLIC ${Boost_INCLUDE_DIR} PRIVATE ../utils)

# target_link_libraries(devcore PUBLIC aleth-buildinfo Boost::filesystem Boost::system Boost::log Boost::thread Threads::Threads PRIVATE ethash)
target_link_libraries(devcore PUBLIC aleth-buildinfo Boost::filesystem Boost::system Boost::log Boost::thread Threads::Threads ethash)

find_package(LevelDB)
target_include_directories(devcore SYSTEM PUBLIC ${LEVELDB_INCLUDE_DIRS})
target_link_libraries(devcore PRIVATE ${LEVELDB_LIBRARIES})
