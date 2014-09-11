include_directories(
    ../include
)

add_library(sqlitehpp STATIC sqlite.cpp)

target_link_libraries(sqlitehpp
    sqlite3
)
