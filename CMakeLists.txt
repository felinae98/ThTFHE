cmake_minimum_required(VERSION 3.10)

project(ThTFHE)

add_subdirectory(OpenBLAS)
add_subdirectory(tfhe/src)

get_target_property(TFHE_SOURCE tfhe-spqlios-fma SOURCES)
get_target_property(OpenBLAS_SOURCE openblas SOURCES)

add_library(thfhe SHARED src/libthfhe.cpp src/thfhe.hpp)
target_link_libraries(thfhe openblas)

add_executable(keygen src/KeyGen.cpp ${TFHE_SOURCE})

add_executable(convert src/Convert.cpp src/threshold_decryption_functions.cpp ${TFHE_SOURCE} ${OpenBLAS_SOURCE})

add_executable(tlwetn src/threshold_decryption_functions.cpp src/TLwe_TN.cpp ${TFHE_SOURCE} ${OpenBLAS_SOURCE})
