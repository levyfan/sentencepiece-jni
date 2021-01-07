cmake_minimum_required(VERSION 3.1)
project(sentencepiece-jni)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_POSITION_INDEPENDENT_CODE ON)

include(ExternalProject)

if (MSVC)
  if (NOT JAVA_HOME)
    message(FATAL_ERROR
      "sentencepiece-jni requires JAVA_HOME to be defined for Windows builds.")
  endif()
  message("JAVA_HOME is ${JAVA_HOME}")
  set(JNI_HEADERS ${JAVA_HOME}/include)
  set(sentencepiece_STATIC_LIBRARIES ${CMAKE_CURRENT_BINARY_DIR}/sentencepiece/src/sentencepiece-build/src/Release/sentencepiece.lib)
  set(CMAKE_CACHE_ARGS
        -DCMAKE_POSITION_INDEPENDENT_CODE:BOOL=ON
        -DCMAKE_BUILD_TYPE:STRING=Release
        -DSPM_BUILD_TEST:BOOL=ON
        -DSPM_ENABLE_SHARED:BOOL=OFF
  )
else()
  find_package(JNI)
  set(JNI_HEADERS ${JNI_INCLUDE_DIRS})
  set(sentencepiece_STATIC_LIBRARIES ${CMAKE_CURRENT_BINARY_DIR}/sentencepiece/src/sentencepiece-build/src/libsentencepiece.a)
  set(CMAKE_CACHE_ARGS
           -DCMAKE_POSITION_INDEPENDENT_CODE:BOOL=ON
           -DCMAKE_BUILD_TYPE:STRING=Release
  )
endif()

set(sentencepiece_INCLUDE_DIRS ${CMAKE_CURRENT_BINARY_DIR}/sentencepiece/src/sentencepiece/src)
ExternalProject_Add(sentencepiece
    PREFIX sentencepiece
    GIT_REPOSITORY https://github.com/google/sentencepiece.git
    GIT_TAG v0.1.92
    INSTALL_COMMAND ""
    CMAKE_CACHE_ARGS ${CMAKE_CACHE_ARGS}
)

add_library(sentencepiece_jni SHARED com_github_google_sentencepiece_SentencePieceJNI.cc)
add_dependencies(sentencepiece_jni sentencepiece)
set_target_properties(sentencepiece_jni PROPERTIES WINDOWS_EXPORT_ALL_SYMBOLS ON)
target_include_directories(sentencepiece_jni PUBLIC
    ${JNI_HEADERS}
    ${sentencepiece_INCLUDE_DIRS})
target_link_libraries(sentencepiece_jni ${sentencepiece_STATIC_LIBRARIES})

if (MSVC)
  string(REPLACE "/MD" "/MT" CMAKE_CXX_FLAGS_DEBUG          ${CMAKE_CXX_FLAGS_DEBUG})
  string(REPLACE "/MD" "/MT" CMAKE_CXX_FLAGS_MINSIZEREL     ${CMAKE_CXX_FLAGS_MINSIZEREL})
  string(REPLACE "/MD" "/MT" CMAKE_CXX_FLAGS_RELEASE        ${CMAKE_CXX_FLAGS_RELEASE})
  string(REPLACE "/MD" "/MT" CMAKE_CXX_FLAGS_RELWITHDEBINFO ${CMAKE_CXX_FLAGS_RELWITHDEBINFO})
  add_definitions("/wd4267 /wd4244 /wd4305 /Zc:strictStrings /utf-8")
endif()

install(TARGETS sentencepiece_jni DESTINATION ${CMAKE_INSTALL_PREFIX})
