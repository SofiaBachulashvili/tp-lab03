# Лабораторная работа 3. ИУ8-24 Бачулашвили София

# tp-lab03

```sh
❯ export GITHUB_USERNAME=SofiaBachulashvili 
❯ cd ${GITHUB_USERNAME}/workspace
❯ pushd .
 ~/SofiaBachulashvili/workspace  ~/SofiaBachulashvili/workspace
 
 source scripts/activate
 ```
 
 ```sh
❯ git clone git@github.com:SofiaBachulashvili/tp-lab02.git projects/lab03
Клонирование в «projects/lab03»...
remote: Enumerating objects: 22, done.
remote: Counting objects: 100% (22/22), done.
remote: Compressing objects: 100% (16/16), done.
remote: Total 22 (delta 2), reused 11 (delta 0), pack-reused 0
Получение объектов: 100% (22/22), 7.56 КиБ | 7.56 МиБ/с, готово.
Определение изменений: 100% (2/2), готово.
                                                                                                       
❯ cd projects/lab03                                                                                             

❯ git branch -M main

❯ git remote add origin git@github.com:SofiaBachulashvili/tp-lab03.git                                              
```

```sh                                                                                       
❯ g++ -std=c++11 -I./include -c sources/print.cpp
                                                                                   
❯ ls print.o
print.o
                                                                                   
❯ nm print.o | grep print
0000000000000000 T _Z5printRKNSt7__cxx1112basic_stringIcSt11char_traitsIcESaIcEEERSo
0000000000000026 T _Z5printRKNSt7__cxx1112basic_stringIcSt11char_traitsIcESaIcEEERSt14basic_ofstreamIcS2_E                                                                                                                                                                 
```

```sh                                                                                
❯ ar rvs print.a print.o 
ar: создаётся print.a
a - print.o
                                                                                     
❯ file print.a
print.a: current ar archive
                                                                                     
❯ g++ -std=c++11 -I./include -c examples/example1.cpp 
                                                                                   
❯ ls example1.o 
example1.o
                                                                                  
❯ g++ example1.o print.a -o example1
                                                                                    
❯ ./example1 && echo 
hello
                                                                                
❯ g++ -std=c++11 -I./include -c examples/example2.cpp
```

```sh                                                                                     
❯ nm example2.o
                 U __gxx_personality_v0
0000000000000000 T main
                 U _Unwind_Resume
                 U _Z5printRKNSt7__cxx1112basic_stringIcSt11char_traitsIcESaIcEEERSt14basic_ofstreamIcS2_E
                 U _ZNSt14basic_ofstreamIcSt11char_traitsIcEEC1EPKcSt13_Ios_Openmode
                 U _ZNSt14basic_ofstreamIcSt11char_traitsIcEED1Ev
0000000000000000 W _ZNSt15__new_allocatorIcED1Ev
0000000000000000 W _ZNSt15__new_allocatorIcED2Ev
0000000000000000 n _ZNSt15__new_allocatorIcED5Ev
                 U _ZNSt7__cxx1112basic_stringIcSt11char_traitsIcESaIcEEC1EPKcRKS3_
                 U _ZNSt7__cxx1112basic_stringIcSt11char_traitsIcESaIcEED1Ev
                 U _ZSt21ios_base_library_initv
0000000000000000 r _ZStL19piecewise_construct
```

```sh                                                                                    
❯ g++ example2.o print.a -o example2
                                                                                    
❯ ./example2                        
                                                                                     
❯ cat log.txt && echo 
hello
```

```sh                                                                                    
❯ rm -rf example1.o example2.o print.o
                                                                                    
❯ rm -rf print.a
                                                                                    
❯ rm -rf example1 example2
                                                                                  
❯ rm -rf log.txt
```

```sh                                                                                      
❯ cat > CMakeLists.txt <<EOF
cmake_minimum_required(VERSION 3.4)
project(print)
EOF

                                                                                     
❯ cat >> CMakeLists.txt <<EOF
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
EOF

                                                                                    
❯ cat >> CMakeLists.txt <<EOF
add_library(print STATIC \${CMAKE_CURRENT_SOURCE_DIR}/sources/print.cpp)
EOF

                                                                                   
❯ cat >> CMakeLists.txt <<EOF
include_directories(\${CMAKE_CURRENT_SOURCE_DIR}/include)
EOF
```

```sh                                                                                  
❯ cmake -H. -B_build -G "Unix Makefiles" 
CMake Deprecation Warning at CMakeLists.txt:1 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.
CMake Deprecation Warning at CMakeLists.txt:1 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.


-- The C compiler identification is GNU 14.0.1
-- The CXX compiler identification is GNU 14.0.1
-- Detecting C compiler ABI info
-- Detecting C compiler ABI info - done
-- Check for working C compiler: /usr/bin/cc - skipped
-- Detecting C compile features
-- Detecting C compile features - done
-- Detecting CXX compiler ABI info
-- Detecting CXX compiler ABI info - done
-- Check for working CXX compiler: /usr/bin/c++ - skipped
-- Detecting CXX compile features
-- Detecting CXX compile features - done
-- Configuring done (1.7s)
-- Generating done (0.0s)
-- Build files have been written to: /home/sofia/SofiaBachulashvili/workspace/projects/lab03/_build
```

```sh                                                                                     
❯ cmake --build _build
[ 50%] Building CXX object CMakeFiles/print.dir/sources/print.cpp.o
[100%] Linking CXX static library libprint.a
[100%] Built target print
```

```sh                                                                                     
❯ cat >> CMakeLists.txt <<EOF

add_executable(example1 \${CMAKE_CURRENT_SOURCE_DIR}/examples/example1.cpp)
add_executable(example2 \${CMAKE_CURRENT_SOURCE_DIR}/examples/example2.cpp)
EOF
                                                                                   
❯ cat >> CMakeLists.txt <<EOF

target_link_libraries(example1 print)
target_link_libraries(example2 print)
EOF
```

```sh                                                                               
❯ cmake --build _build
CMake Deprecation Warning at CMakeLists.txt:1 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.


-- Configuring done (0.0s)
-- Generating done (0.0s)
-- Build files have been written to: /home/sofia/SofiaBachulashvili/workspace/projects/lab03/_build
[ 33%] Built target print
[ 50%] Building CXX object CMakeFiles/example1.dir/examples/example1.cpp.o
[ 66%] Linking CXX executable example1
[ 66%] Built target example1
[ 83%] Building CXX object CMakeFiles/example2.dir/examples/example2.cpp.o
[100%] Linking CXX executable example2
[100%] Built target example2
```

```sh
❯ cmake --build _build --target print 
[100%] Built target print
```

```sh                                                                                    
❯ cmake --build _build --target example1
[ 50%] Built target print
[100%] Built target example1
                                                                                    
❯ cmake --build _build --target example2
[ 50%] Built target print
[100%] Built target example2
```

```sh                                                                                
❯ ls -la _build/libprint.a 
-rw-r--r--. 1 sofia sofia 2254 апр 29 21:20 _build/libprint.a
                                                                                     
❯ _build/example1 && echo hello
hellohello
                                                                                                                                                                                                                                                 
❯  _build/example2
cat log.txt && echo hello 
hellohello
                                                                                  
❯ rm -rf log.txt
```

```sh                                                                                 
❯ git clone https://github.com/tp-labs/lab03 tmp 
Клонирование в «tmp»...
remote: Enumerating objects: 91, done.
remote: Counting objects: 100% (30/30), done.
remote: Compressing objects: 100% (9/9), done.
remote: Total 91 (delta 23), reused 21 (delta 21), pack-reused 61
Получение объектов: 100% (91/91), 1.02 МиБ | 685.00 КиБ/с, готово.
Определение изменений: 100% (41/41), готово.
                                                                            
❯ mv -f tmp/CMakeLists.txt .
                                                                                  
❯ rm -rf tmp
```

```sh                                                                                
❯ cat CMakeLists.txt
cmake_minimum_required(VERSION 3.4)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

option(BUILD_EXAMPLES "Build examples" OFF)

project(print)

add_library(print STATIC ${CMAKE_CURRENT_SOURCE_DIR}/sources/print.cpp)

target_include_directories(print PUBLIC
  $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include>
  $<INSTALL_INTERFACE:include>
)

if(BUILD_EXAMPLES)
  file(GLOB EXAMPLE_SOURCES "${CMAKE_CURRENT_SOURCE_DIR}/examples/*.cpp")
  foreach(EXAMPLE_SOURCE ${EXAMPLE_SOURCES})
    get_filename_component(EXAMPLE_NAME ${EXAMPLE_SOURCE} NAME_WE)
    add_executable(${EXAMPLE_NAME} ${EXAMPLE_SOURCE})
    target_link_libraries(${EXAMPLE_NAME} print)
    install(TARGETS ${EXAMPLE_NAME}
      RUNTIME DESTINATION bin
    )
  endforeach(EXAMPLE_SOURCE ${EXAMPLE_SOURCES})
endif()

install(TARGETS print
    EXPORT print-config
    ARCHIVE DESTINATION lib
    LIBRARY DESTINATION lib
)

install(DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}/include/ DESTINATION include)
install(EXPORT print-config DESTINATION cmake)
```

```sh                                                                                   
❯ cmake -H. -B_build -DCMAKE_INSTALL_PREFIX=_install  
CMake Deprecation Warning at CMakeLists.txt:1 (cmake_minimum_required):
  Compatibility with CMake < 3.5 will be removed from a future version of
  CMake.

  Update the VERSION argument <min> value or use a ...<max> suffix to tell
  CMake that the project does not need compatibility with older versions.


-- Configuring done (0.0s)
-- Generating done (0.0s)
-- Build files have been written to: /home/sofia/SofiaBachulashvili/workspace/projects/lab03/_build
```

```sh                                                                             
❯ cmake --build _build --target install 
[100%] Built target print
Install the project...
-- Install configuration: ""
-- Installing: /home/sofia/SofiaBachulashvili/workspace/projects/lab03/_install/lib/libprint.a
-- Installing: /home/sofia/SofiaBachulashvili/workspace/projects/lab03/_install/include
-- Installing: /home/sofia/SofiaBachulashvili/workspace/projects/lab03/_install/include/print.hpp
-- Installing: /home/sofia/SofiaBachulashvili/workspace/projects/lab03/_install/cmake/print-config.cmake
-- Installing: /home/sofia/SofiaBachulashvili/workspace/projects/lab03/_install/cmake/print-config-noconfig.cmake
```

```sh                                                                                   
❯ tree _install 
_install
├── cmake
│   ├── print-config.cmake
│   └── print-config-noconfig.cmake
├── include
│   └── print.hpp
└── lib
    └── libprint.a

4 directories, 4 files
```

```sh                                                                              
❯ git add CMakeLists.txt
                                                                                   
❯ git commit -m "added CMakeLists.txt"
[main fb52893] added CMakeLists.txt
 1 file changed, 36 insertions(+)
 create mode 100644 CMakeLists.txt
                                                                                  
❯ git push -u origin main             
Перечисление объектов: 4, готово.
Подсчет объектов: 100% (4/4), готово.
При сжатии изменений используется до 12 потоков
Сжатие объектов: 100% (3/3), готово.
Запись объектов: 100% (3/3), 781 байт | 390.00 КиБ/с, готово.
Total 3 (delta 1), reused 0 (delta 0), pack-reused 0 (from 0)
remote: Resolving deltas: 100% (1/1), completed with 1 local object.
To github.com:SofiaBachulashvili/tp-lab03.git
   9efad30..fb52893  main -> main
branch 'main' set up to track 'origin/main'.
```
